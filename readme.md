
# To import products.json in mongoDB
-mongoimport --db products --collection items --file products.json --port 27017  --jsonArray

#  show dbs

admin       41 kB
airbnb    54.7 MB
config    36.9 kB
local     73.7 kB
masai      283 kB
movies     123 kB
products   106 kB

# use products as database
- use products
switched to db products
products> show collections
items
products>


# 1. top 10 purchased items

- db.items.find({}).sort({no_of_purchases: -1}).limit(10)

**Output->**
[
  {
    _id: ObjectId("6207cf3c18ceb84167447fd6"),
    product_name: 'Pork - Ham Hocks - Smoked',
    product_id: 775,
    product_rating: 4,
    currency: 'Rupiah',
    price: 246,
    no_of_purchases: 1000,
    qty_left: 711
  },
  {
    _id: ObjectId("6207cf3c18ceb841674480b6"),
    product_name: 'Cod - Black Whole Fillet',
    product_id: 1000,
    product_rating: 10,
    currency: 'Boliviano',
    price: 295,
    no_of_purchases: 999,
    qty_left: 822
  },
  .............
  .........
  ......
  ....
**Below Picture for above query**
-243
-244


# 2. top 10 cheapest items

-  db.items.find({}).sort({price: 1}).limit(10)

**Output->**
[
  {
    _id: ObjectId("6207cf3c18ceb84167447d63"),
    product_name: 'Cucumber - Pickling Ontario',
    product_id: 148,
    product_rating: 5,
    currency: 'Lari',
    price: 101,
    no_of_purchases: 194,
    qty_left: 69
  },
  {
    _id: ObjectId("6207cf3c18ceb84167448060"),
    product_name: 'Cup - Translucent 7 Oz Clear',
    product_id: 912,
    product_rating: 6,
    currency: 'Yen',
    price: 101,
    no_of_purchases: 708,
    qty_left: 919
  },
  {
   .............
  .........
  ......
  ....
**Below Picture for above query**
-245
-246


# 3. top items where qty remains in stock.

- db.items.find({},{qty_left: 1}).sort({price: -1})

**Output->**
[
  { _id: ObjectId("6207cf3c18ceb84167447f0e"), qty_left: 990 },
  { _id: ObjectId("6207cf3c18ceb84167447f55"), qty_left: 89 },
  { _id: ObjectId("6207cf3c18ceb841674480ba"), qty_left: 871 },
  { _id: ObjectId("6207cf3c18ceb84167447de8"), qty_left: 821 },
  { _id: ObjectId("6207cf3c18ceb84167447cf7"), qty_left: 919 },
  { _id: ObjectId("6207cf3c18ceb84167447eb9"), qty_left: 510 },
  { _id: ObjectId("6207cf3c18ceb84167447f84"), qty_left: 444 },
  { _id: ObjectId("6207cf3c18ceb84167447ff0"), qty_left: 614 },
  { _id: ObjectId("6207cf3c18ceb84167447d40"), qty_left: 358 },
  { _id: ObjectId("6207cf3c18ceb84167447e6e"), qty_left: 155 },
  { _id: ObjectId("6207cf3c18ceb84167447ff7"), qty_left: 196 },
  { _id: ObjectId("6207cf3c18ceb84167447cfe"), qty_left: 635 },
  { _id: ObjectId("6207cf3c18ceb84167447eb2"), qty_left: 294 },
  { _id: ObjectId("6207cf3c18ceb84167447e09"), qty_left: 830 },
  { _id: ObjectId("6207cf3c18ceb84167448089"), qty_left: 31 },
  { _id: ObjectId("6207cf3c18ceb84167447f07"), qty_left: 821 },
  { _id: ObjectId("6207cf3c18ceb84167447f6d"), qty_left: 503 },
  { _id: ObjectId("6207cf3c18ceb84167447d13"), qty_left: 631 },
  { _id: ObjectId("6207cf3c18ceb84167447d95"), qty_left: 119 },
  { _id: ObjectId("6207cf3c18ceb84167447e93"), qty_left: 671 }
]
Type "it" for more

- db.items.find({},{qty_left: 1}).sort({price: -1}).count()

**output->**
1000

**Below Picture for above query**
-247


# 4. top 10 rated products.

- db.items.find({},{product_rating: 1}).sort({product_rating: -1}).limit(10)

**Output->**
[
  { _id: ObjectId("6207cf3c18ceb84167447cf5"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447d11"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447d1d"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447ce3"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447cd4"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447d1a"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447d22"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447d1e"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447cff"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447cf4"), product_rating: 10 }
]

**Below Picture for above query**
-248


# 5. bottom 10 rated products.

- db.items.find({},{product_rating: 1}).sort({product_rating: 1}).limit(10)

**Output->**
[
  { _id: ObjectId("6207cf3c18ceb84167447d02"), product_rating: 1 },
  { _id: ObjectId("6207cf3c18ceb84167447d19"), product_rating: 1 },
  { _id: ObjectId("6207cf3c18ceb84167447d35"), product_rating: 1 },
  { _id: ObjectId("6207cf3c18ceb84167447d05"), product_rating: 1 },
  { _id: ObjectId("6207cf3c18ceb84167447cfb"), product_rating: 1 },
  { _id: ObjectId("6207cf3c18ceb84167447d2a"), product_rating: 1 },
  { _id: ObjectId("6207cf3c18ceb84167447d44"), product_rating: 1 },
  { _id: ObjectId("6207cf3c18ceb84167447d36"), product_rating: 1 },
  { _id: ObjectId("6207cf3c18ceb84167447d15"), product_rating: 1 },
  { _id: ObjectId("6207cf3c18ceb84167447cd9"), product_rating: 1 }
]

**Below Picture for above query**
-249


# 6. from 11-20 top rated products.

- db.items.find({},{product_rating: 1}).sort({product_rating: -1}).limit(10).skip(10)

**Output->**
[
  { _id: ObjectId("6207cf3c18ceb84167447d48"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447d1a"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447d52"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447d1e"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447d54"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447d76"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447d75"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447d24"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447d22"), product_rating: 10 },
  { _id: ObjectId("6207cf3c18ceb84167447cf4"), product_rating: 10 }
]

**Below Picture for above query**
-250


# 7. find products with rating between 3 and 4, and sorted from descending order of rating, if the ratings are same, then show the alphabetic order of name of the product.

- db.items.find({product_rating: {$in:[3,4]}}).sort({product_rating: -1,product_name: 1}).count()

**Output->** 222

- db.items.find({product_rating: {$in:[3,4]}}).sort({product_rating: -1,product_name: 1})

**Output->**
[
  {
    _id: ObjectId("6207cf3c18ceb84167447e29"),
    product_name: 'Allspice - Jamaican',
    product_id: 344,
    product_rating: 4,
    currency: 'Lempira',
    price: 717,
    no_of_purchases: 35,
    qty_left: 376
  },
  {
    _id: ObjectId("6207cf3c18ceb84167447ed5"),
    product_name: 'Anchovy Fillets',
    product_id: 512,
    product_rating: 4,
    currency: 'Pound',
    price: 498,
    no_of_purchases: 274,
    qty_left: 37
  },
  {
  .............
  .........
  ......
  ....
**Below Picture for above query**
-251
-252