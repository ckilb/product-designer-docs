---
nav_order: 200
parent: FAQ
---

# I've got a lot of articles. Do I really need to specify all the article numbers in the configuration?

If you have a lot of articles and you want to use the same configuration for all of them you can also use wildcards.
So let's assume you have five articles with the following article numbers:
- `TSHIRT_A`
- `TSHIRT_B`
- `TSHIRT_C`
- `TSHIRT_1`
- `TSHIRT_2`

In your configuration - instead of adding all five article numbers - you could simply add `TSHIRT_*`.

If the configuration has to be different for these articles you have to create a new configuration for each article and assign
the article number directly. This could mean a lot of work - but it's something that has to be done.
In that case, please mind that you can first create a single configuration and then **copy** that configuration and only change some of the fields.
Also you could use the **import/export functionality** to export all your configuration in a CSV file which you can edit locally and upload it afterwards again.
