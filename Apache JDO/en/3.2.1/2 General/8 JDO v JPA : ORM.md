[TOC]

There are 2 prevalent specification in the Java ORM world. JDO provides the most complete definition, whilst JPA is the most recent.

### Relationships

In this guide we show the different types of ORM relation commonly used, and mark against it which specification supports it. This list is not yet complete but will be added to to provide a comprehensive list of relationship type and where you can find it.


| Field Type    | Relation                                                                                                                                             | JDO | JPA |
|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------|---|-----|
| `PC`           | [1-1 Unidirectional](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_one.html#uni)                                                 | ✅ | ✅   |
| `PC`           | [1-1 Bidirectional](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_one.html#bi)                                                   | ✅ | ✅   |
| `PC`           | [1-1 serialised](http://www.datanucleus.org/products/accessplatform/jdo/orm/serialised.html#PC)                                                      |✅  | ✅   |
| `PC`           | [1-1 CompoundIdentity Unidirectional](http://www.datanucleus.org/products/accessplatform/jdo/orm/compound_identity.html#1_1_uni)                     |  ✅| ✅   |
| `PC`           | [1-N CompoundIdentity Collection Bidirectional](http://www.datanucleus.org/products/accessplatform/jdo/orm/compound_identity.html#1_N_coll_bi)       |  ✅| ✅   |
| `PC`           | [1-N CompoundIdentity Map Bidirectional](http://www.datanucleus.org/products/accessplatform/jdo/orm/compound_identity.html#1_N_map_bi)               | ✅ | ❌   |
| `Interface`    | [1-1 Unidirectional](http://www.datanucleus.org/products/accessplatform/jdo/orm/interfaces.html)                                                     | ✅ | ❌   |
| `Interface`    | [1-1 Bidirectional](http://www.datanucleus.org/products/accessplatform/jdo/orm/interfaces.html)                                                      | ✅ | ❌   |
| `Interface`    | [1-1serialised](http://www.datanucleus.org/products/accessplatform/jdo/orm/serialised.html#Reference)                                                | ✅ | ?   |
| `Collection<PC>` | [1-N ForeignKey Unidirectional Collection](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_collection.html#fk_uni)            |  ✅|  ✅|
| `Collection<PC>` | [1-N ForeignKey Bidirectional Collection](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_collection.html#fk_bi)              |  ✅| ✅ |
| `Collection<PC>` | [1-N JoinTable Unidirectional Collection](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_collection.html#join_uni)           |  ✅| ✅ |
| `Collection<PC>` | [1-N JoinTable Bidirectional Collection](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_collection.html#join_bi)             |  ✅|  ✅|
| `Collection<Non-PC>` | [1-N JoinTable Collection](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_collection.html#join_nonpc)                        |  ✅|✅  |
| `Collection<PC>` | [1-N JoinTable Collection using shared JoinTable](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_collection.html#shared_join) | ❌                  | ❌                                                                                                                                                     |
| `Collection<PC>` | [1-N ForeignKey Collection using shared ForeignKey](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_collection.html#shared_fk)|  ❌|  ❌|
| `Collection<PC>` | [M-N JoinTable](http://www.datanucleus.org/products/accessplatform/jdo/orm/many_to_many.html)|  ✅|  ✅|
| `Collection<PC>` | [1-N CompoundIdentity Unidirectional](http://www.datanucleus.org/products/accessplatform/jdo/orm/compound_identity.html#1_N_uni)|  ✅| ✅ |
| `Collection<PC>` | [1-N serialised Collection](http://www.datanucleus.org/products/accessplatform/jdo/orm/serialised.html#Collection)|  ✅| ✅ |
| `Collection<PC>` | [1-N JoinTable Collection of serialised elements](http://www.datanucleus.org/products/accessplatform/jdo/orm/serialised.html#CollectionElements)|  ✅|❌  |
| `List<PC>`     | [1-N ForeignKey Unidirectional Indexed List](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_list.html#fk_uni)|  ✅|✅  |
| `List<PC>`| [1-N ForeignKey Bidirectional Indexed List](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_list.html#fk_bi)|  ✅|✅  |
| `List<PC>`| [1-N JoinTable Unidirectional Indexed List](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_list.html#join_uni)|  ✅|✅  |
| `List<PC>`| [1-N JoinTable Bidirectional Indexed List](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_list.html#join_bi)|  ✅|✅  |
| `List<Non-PC>`| [1-N JoinTable Indexed List](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_list.html#join_nonpc)|  ✅| ✅ |
| `List<PC>`| [1-N ForeignKey Unidirectional Ordered List](http://www.datanucleus.org/products/accessplatform/jpa/orm/one_to_many_list.html#fk_uni)|  ❌|  ✅|
| `List<PC>`| [1-N ForeignKey Bidirectional Ordered List](http://www.datanucleus.org/products/accessplatform/jpa/orm/one_to_many_list.html#fk_bi)|  ❌|  ✅|
| `List<PC>`| [1-N JoinTable Unidirectional Ordered List](http://www.datanucleus.org/products/accessplatform/jpa/orm/one_to_many_list.html#join_uni)|  ❌|  ✅|
| `List<PC>`| [1-N JoinTable Bidirectional Ordered List](http://www.datanucleus.org/products/accessplatform/jpa/orm/one_to_many_list.html#join_bi)|  ❌|  ✅|
| `Map<PC, PC>`| [1-N JoinTable Map](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_map.html#join_pc_pc)|✅  |  ❌|
| `Map<Non-PC, PC>`| [1-N JoinTable Map](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_map.html#join_simple_pc)|✅  |  ❌|
| `Map<PC, Non-PC>`| [1-N JoinTable Map](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_map.html#join_pc_simple)|✅  |  ❌|
| `Map<Non-PC, Non-PC>`| [1-N JoinTable Map](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_map.html#join_simple_simple)| ✅ | ❌ |
| `Map<Non-PC, PC>`| [1-N ForeignKey Map Unidirectional (key stored in value)](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_map.html#fk_uni_key)|✅  |✅  |
| `Map<Non-PC, PC>`| [1-N ForeignKey Map Bidirectional (key stored in value)](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_map.html#fk_bi_key)| ✅ |✅  |
| `Map<PC, Non-PC>`| [1-N ForeignKey Map Unidirectional (value stored in key)](http://www.datanucleus.org/products/accessplatform/jdo/orm/one_to_many_map.html#fk_uni_value)| ✅ | ❌ |
| `Map<PC, PC>`| [1-N serialised Map](http://www.datanucleus.org/products/accessplatform/jdo/orm/serialised.html#Map)|  ✅| ✅ |
| `Map<PC, PC>`| [1-N JoinTable Map of serialised keys/values](http://www.datanucleus.org/products/accessplatform/jdo/orm/serialised.html#MapKeysValues)| ✅ |❌ |
| PC\[ \]| [1-N ForeignKey Unidirectional Array](http://www.datanucleus.org/products/accessplatform/jdo/orm/arrays.html#fk)| ✅ |  ❌|
| PC\[ \] | [1-N JoinTable Unidirectional Array](http://www.datanucleus.org/products/accessplatform/jdo/orm/arrays.html#join)|✅  | ❌ |
| PC\[ \] | [1-N serialised Array](http://www.datanucleus.org/products/accessplatform/jdo/orm/serialised.html#Array)| ✅ |  ✅|
| Non-PC\[ \] | [1-N JoinTable Unidirectional Array](http://www.datanucleus.org/products/accessplatform/jdo/orm/arrays.html#join)|✅  | ❌ |
