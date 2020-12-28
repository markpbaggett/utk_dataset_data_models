Understanding External Relationships
====================================

The :code:`RELS-EXT` binary, or **"RELATIONSHIPS EXTERNAL,"** serves as our structural metadata file. It describes how
parts of a dataset relate to the dataset.  For this reason, it is essential to migration.

For example, let's look at dataset `utk.ir.fg:2179 <https://trace.utk.edu/islandora/object/utk.ir.fg%3A2179>`_. This
dataset consists of eight files with seven restricted from public access.

Dataset Objects
---------------

**utk.ir.fg:2179** has structural metadata that describes it in its :code:`RELS-EXT` binary.

.. code-block:: turtle

    @prefix fedora: <info:fedora/fedora-system:def/relations-external#> .
    @prefix fedora-model: <info:fedora/fedora-system:def/model#> .
    @prefix islandora: <http://islandora.ca/ontology/relsext#> .

    <info:fedora/utk.ir.fg:2179> islandora:inheritXacmlFrom <info:fedora/utk.ir:fg> ;
        fedora-model:hasModel <info:fedora/islandora:compoundCModel> ;
        fedora:isMemberOfCollection <info:fedora/utk.ir:fg> .

You can tell this is a dataset because its :code:`fedora-model:hasModel` object is :code:`<info:fedora/islandora:compoundCModel>`.
All dataset objects have this model. Furthermore, all datasets have a :code:`fedora:isMemberOfCollection` of
:code:`<info:fedora/utk.ir:fg>`. We consider the other triple to be noise and not meaningful
(:code:`<info:fedora/utk.ir.fg:2179> islandora:inheritXacmlFrom <info:fedora/utk.ir:fg> .`)

Parts of Datasets
-----------------

Every piece of a dataset is also a Fedora object with a :code:`RELS-EXT` binary with a triple that describes its
relationship to the parent object.

.. code-block:: turtle
    :emphasize-lines: 9

    @prefix ns0: <info:fedora/fedora-system:def/relations-external#> .
    @prefix ns1: <info:fedora/fedora-system:def/model#> .
    @prefix ns2: <http://islandora.ca/ontology/relsext#> .

    <info:fedora/utk.ir.fg:2180>
      ns0:isMemberOfCollection <info:fedora/utk.ir:fg> ;
      ns1:hasModel <info:fedora/islandora:binaryObjectCModel> ;
      ns2:inheritXacmlFrom <info:fedora/utk.ir:fg> ;
      ns0:isConstituentOf <info:fedora/utk.ir.fg:2179> ;
      ns2:isSequenceNumberOfutk.ir.fg_2179 "1" ;
      ns2:isManageableByUser "admin", "bdysonsm", "ceaker", "mbagget1", "fedoraAdmin" ;
      ns2:isManageableByRole "administrator", "dataset_manager_role" .

All parts have a :code:`<info:fedora/utk.ir.fg:2180> ns1:hasModel <info:fedora/islandora:binaryObjectCModel> .` triple
that indicates the object has a content model that makes it a part of a data set. We don't consider sequences here to be
important nor is it important to indicate the part is attached to the larger collection. The
:code:`<info:fedora/utk.ir.fg:2180> ns2:isManageableByRole "administrator", "dataset_manager_role" .` indicates the
object should only be managed by users with these roles.  The :code:`ns2:isManageableByUser` triple is there for precautions
but not considered important for migration.  Furthermore, this information is described in a XACML policy described else
where in this document.

Let's also take a look at a :code:`RELS-EXT` for a restricted from view part.

.. code-block:: turtle
    :emphasize-lines: 9, 10

    @prefix ns0: <info:fedora/fedora-system:def/relations-external#> .
    @prefix ns1: <info:fedora/fedora-system:def/model#> .
    @prefix ns2: <http://islandora.ca/ontology/relsext#> .

    <info:fedora/utk.ir.fg:2181>
      ns0:isMemberOfCollection <info:fedora/utk.ir:fg> ;
      ns1:hasModel <info:fedora/islandora:binaryObjectCModel> ;
      ns2:inheritXacmlFrom <info:fedora/utk.ir:fg> ;
      ns2:isViewableByUser "admin", "ceaker", "mbagget1", "fedoraAdmin" ;
      ns2:isViewableByRole "administrator", "dataset_manager_role" ;
      ns2:isManageableByUser "admin", "ceaker", "mbagget1", "fedoraAdmin" ;
      ns2:isManageableByRole "administrator", "dataset_manager_role" ;
      ns0:isConstituentOf <info:fedora/utk.ir.fg:2179> ;
      ns2:isSequenceNumberOfutk.ir.fg_2179 "2" .

In this example, the triples are mostly the same except there are two triples that describe who can "see" this part.
We consider the :code:`ns2:isManageableByRole` to be meaningful for migration, but the other triple is there currently
as a precaution.  As stated above, access restrictions are managed in a XACML policy described elsewhere.