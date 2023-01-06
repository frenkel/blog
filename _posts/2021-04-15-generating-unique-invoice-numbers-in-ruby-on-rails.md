---
layout: post
title: "Generating unique invoice numbers in Ruby on Rails"
description: "In some countries it is required for invoice numbers to be unique and sequential. Let me show you how to build a solid generator yourself if you don't want to use the simple primary keys format."
date: 2021-04-15 11:20:04 +0200
comments: true
categories: Programming
---

I'm currently building a subscription tracker with reminders. While building the subscription part of this service I of course need to generate invoices. In The Netherlands we're required to have a unique invoice number on them. How do you build something like that in Ruby on Rails?

We first need to validate that the numbers we store are actually unique. Validations in Ruby have some race conditions, where two might be generated at the same time without either one noticing. So, there is only one place where you can be sure of uniqueness: in the database. I've added a unique index on the invoice number column to fail hard if something might generate a duplicate.

<pre>add_index :invoices, :number, unique: true</pre>

Next we need to build the actual generation of unique numbers. I've chosen to build an InvoiceService which is responsible for creating invoices and generating unique numbers. The numbers are in the format of year-number, for example 2021-123. For this I've made a function that that looks up the previous invoice number parts. Something like this works:

<pre>
  def last_invoice_number_parts
    current_year = Time.zone.now.year.to_s
    last_invoice = Invoice.order(Arel.sql('substring(number from 6)::int')).last

    if last_invoice&.number&.start_with?(current_year)
      last_invoice.number.split('-')
    else
      [current_year, 0]
    end
  end
</pre>

Now the tricky part, how do we generate a new number and make sure it's unique when stored? Regenerate and save again when you catch the ActiveRecord::RecordNotUnique exception on save. If that happens it means we need to generate a new incremented number and should thus try again. Something like this should work:

<pre>
  def generate_invoice_number
    parts = last_invoice_number_parts
    @invoice.number = "#{parts.first}-#{parts.last.to_i + 1}"
    @invoice.save!
  rescue ActiveRecord::RecordNotUnique
    retry # another database record was just with the same number
  end
</pre>

That's it. Let's hope this function will generate a lot of unique invoice numbers for us!
