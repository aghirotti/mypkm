---
alias: uuid
---

### What is UUID?

A UUID (Universal Unique Identifier) is a 128-bit value used to uniquely identify an object or entity on the internet. Depending on the specific mechanisms used, a UUID is either guaranteed to be different or is, at least, extremely likely to be different from any other UUID generated until A.D. 3400.

UUIDs can be generated to refer to almost anything imaginable. For example, they can identify databases, system instances, primary keys, Bluetooth profiles or [objects](https://www.techtarget.com/searchapparchitecture/definition/object) with short lifetimes.

### [Why should you care](https://www.cockroachlabs.com/blog/what-is-a-uuid/)?

When working with a database, it’s common practice to use some kind of `id` field to provide a unique identifier for each row in a table.

Imagine, for example, a `customers` table. We wouldn’t want to use fields such as `name` or `address` as unique identifiers because it’s possible more than one customer could have the same name, or share the same address.

Instead, it’s a good idea to assign each row some kind of unique identifier. One option we have is to use a UUID. A UUID – that’s short for Universally Unique IDentifier, by the way – is a 36-character alphanumeric string that can be used to identify information (such as a table row).

Here is one example of a UUID: `acde070d-8c4c-4f0d-9d8a-162843c10333`

UUIDs are widely used in part because they are highly likely to be unique _globally_, meaning that not only is our row’s UUID unique in our database table, it’s probably the only row with that UUID in any system _anywhere_.

(Technically, it’s not _impossible_ that the same UUID we generate could be used somewhere else, but with 340,282,366,920,938,463,463,374,607,431,768,211,456 different possible UUIDs out there, the chances are _very_ slim).

### Disadvantages of UUIDs![](https://www.cockroachlabs.com/img/cockroach-section-link.svg)

The only significant disadvantage of UUIDs is that they take up 128 bits in memory (and often a bit more when we include metadata). If minimizing storage space is absolutely mission-critical, clearly storing a sequential ID (which will probably range somewhere between 1-10 numeric characters) is going to be more efficient than storing a 36-character alphanumeric.

However, in most cases the disadvantages of using something like a sequential identifier significantly outweigh the minimal increase in storage costs that comes from using UUIDs. UUIDs are extremely popular and widely used for a variety of different identification purposes. We’ve focused on database examples in this article because [we make a pretty awesome database](https://www.cockroachlabs.com/product/), but UUIDs are also used in analytics systems, web and mobile applications, etc.
