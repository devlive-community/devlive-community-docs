[TOC]

The two persistence standards in Java have very similar API’s on the face of it. Here we give a comparison of the method calls and their equivalent in the other API.

| Operation | JDO | JPA |
| --- | --- | --- |
| Persist Object| pm.makePersistent()| em.persist |
| Update Object | pm.makePersistent()| em.merge()|
| Remove Object | pm.deletePersistent()| em.remove()|
| Retrieve Object | pm.getObjectById()<br />pm.getExtent()| em.find()|
| Refresh Object | pm.refresh()| em.refresh()|
| Detach single Object | pm.detachCopy()| em.detach()|
| Flush changes | pm.flush()| em.flush()|
| Access transaction | pm.currentTransaction()| em.getTransaction()|
| New Query| pm.newQuery()| em.createQuery()|
| New Named Query | pm.newNamedQuery()| em.createNamedQuery()|
| New SQL Query | pm.newQuery()| em.createNativeQuery()|
