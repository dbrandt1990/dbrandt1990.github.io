---
layout: post
title:      "ORM having some trouble"
date:       2021-02-25 23:18:21 +0000
permalink:  orm_having_some_trouble
---


ORM, or object-relational mapping, is taking different objects in an application and relating them to one another through ids primary and foreign ids in a database.  All items when stored in the DB are given a primary key, this is a unique identifier to maintain the separation of objects that otherwise could be misconstrued as the "same" object. Foreign keys on the other hand are ids (primary keys) from a different object, that will be stored within the new object to show that they are related.
For example, we need to keep track of all the pets at Hogwarts, so we need to create an object for Harry, and his pet Hedwig. After we create the objects and save them to their respective tables within our DB they will be assigned their ids.


`harry = Person.new(name: "Harry, age: 11)`
`hedwig = Pet.new(name: "Hedwig", type: "owl")`


Once Harry, Hedwig, and their classes are added to the DB they will be assigned a PRIMARY KEY as its id.

`harry.save`
`harry.id => 1 #id from people table in db`

`hedwig.save`
`hedwig.id => 1  #id from pets table  in db`

So we know that Hedwig and Harry go together, but how can we connect the two? This is where the foreign keys come in. We can create an association by adding a column to the people table or the pets table to hold the foreign key of the other item. First, we have to think about the relationship between the two objects, in terms of 
* 	has many
* 	has one
* 	belongs to 
* 	has many :through
* 	has one :through

(the associations above are used almost verbatim in ActiveRecord to build associations, more on that later) 

Harry 'has one' Hedwig, but 'has many' classes
Hedwig  'belongs to' Harry, and if we made an owlery table Hedwig 'has many' owl friends 'through' the owlery 
and if we made a Hogwarts object, we could say Hogwarts has many' students 'through' classes.

Knowing these relational descriptors we can determine the most efficient way to structure the associations between the objects. Let's think, Harry has a name and an age, which would be represented by columns on our table. Harry has one pet, so we would have to add a column for Hedwig's id, we could call it pet_id, but Harry may have more than one pet at some point. We would have to add a new column for this, and I could get messy pretty quickly, not to mention other people may have a different number of pets so the columns from person to person could be drastically different. Someone may have pet_id_5 while another has none.
Hedwig 'belongs to' Harry, and it would be unlikely that Hedwig would end up with multiple owners at any point, so I think it is safe to associate her with Harry via the pets table. We would add a column called owner_id and put Harry's primary key in there. This way if Harry gets another pet, we could add it to the pets table, and give it Harry's id in the owner_id column and everything stays squeaky clean. Now if we wanted to see who Hedwig's owner is we could type:

`Hedwig.owner_id => 1 #id from people table for Harry`

We could easily pull Hedwig's owner from the DB, and it is relatively stable in that we won't be adding columns for multiple owners. This is ORM, and doing it manually is a BEAR! Having to manually input the foreign keys into their tables and maintain consistent associations as the number of objects increases is not sustainable, enter ActiveRecord.

With the associations we talked about we can easily tell a class that any object instantiated through it will have 'x' association. 

`class Pet < ActiveRecord::Base`
 ` belongs_to :person`
`end`
or
`class Class < ActiveRecord::Base`
`has_many :students`
`end`

Now we could easily say

`Hedwig.person = Harry`
or 
`Potions.students => get all of the students for this class`

and they will forever and always be connected, as they should be.

ORM felt pretty convoluted as I was learning it, but understanding how to do it manually gave me so much more respect for ActiveRecord. It is such a relief to know that you can just connect what you need to, using a syntax that makes sense! So understand what's happening under the hood, and then write a thank you card to the devs that built ActiveRecord to improve life for all of us!






