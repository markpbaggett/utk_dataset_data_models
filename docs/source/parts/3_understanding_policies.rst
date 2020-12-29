Understanding Policies
======================

Each dataset and each dataset part has an attached :code:`POLICY` binary.  This file is based on the
`XACML 1.0 <https://www.oasis-open.org/committees/download.php/2406/oasis-xacml-1.0.pdf>`_ specification.  This section
describes how to interpret our :code:`POLICY` binaries and what information is meaningful for migration.

Deny Management Functions
-------------------------

Management of objects including modifying and creating objects is described in our XACML policies in the :code:`Rule[@RuleId="deny-management-functions"][@Effect="Deny"]`
node. The node lists  the actions related to management of content and disallows users to perform these without an exception.
While these nodes include all the functions (aka actions) a user should not be able to perform unless they are excepted in the
:code:`Rule[@RuleId="deny-management-functions"][@Effect="Deny"]/Condition[@FunctionId="urn:oasis:names:tc:xacml:1.0:function:not"]`
node, the actions section :code:`Rule[@RuleId="deny-management-functions"][@Effect="Deny"]/Target` is not relevant
for migration.  This is because the section is meant to be exhaustive and intends to include all actions associated with
creating or modifying content for the repository.

Relevant to migration is the :code:`Rule[@RuleId="deny-management-functions"][@Effect="Deny"]/Condition[@FunctionId="urn:oasis:names:tc:xacml:1.0:function:not"]`
node.  This node includes the roles and users that are allowed to perform management actions and is separated into two
separate :code:`Apply[@FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of"]` sections.

.. code-block:: xml
    :caption: Deny Management Function Exceptions

    <Condition FunctionId="urn:oasis:names:tc:xacml:1.0:function:not">
      <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:or">
        <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
          <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="urn:fedora:names:fedora:2.1:subject:loginId"/>
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">admin</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">mbagget1</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">fedoraAdmin</AttributeValue>
          </Apply>
        </Apply>
        <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
          <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="fedoraRole"/>
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">administrator</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">dataset_manager_role</AttributeValue>
          </Apply>
        </Apply>
      </Apply>
    </Condition>

The first describes the users that are allowed to perform management functions.  This rule is here as a precaution and
isn't important for migration.  By default, two system accounts are added here automatically plus the account of the
person who deposits the object originally.

.. code-block:: xml
    :caption: Deny Management Function - Users Exception
    :emphasize-lines: 3-10

    <Condition FunctionId="urn:oasis:names:tc:xacml:1.0:function:not">
      <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:or">
        <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
          <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="urn:fedora:names:fedora:2.1:subject:loginId"/>
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">admin</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">mbagget1</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">fedoraAdmin</AttributeValue>
          </Apply>
        </Apply>
        <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
          <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="fedoraRole"/>
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">administrator</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">dataset_manager_role</AttributeValue>
          </Apply>
        </Apply>
      </Apply>
    </Condition>

The second section is relevant for migration and describes the roles that should be able to manage the object.

.. code-block:: xml
    :caption: Deny Management Function - Roles Exception
    :emphasize-lines: 11-17

    <Condition FunctionId="urn:oasis:names:tc:xacml:1.0:function:not">
      <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:or">
        <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
          <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="urn:fedora:names:fedora:2.1:subject:loginId"/>
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">admin</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">mbagget1</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">fedoraAdmin</AttributeValue>
          </Apply>
        </Apply>
        <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
          <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="fedoraRole"/>
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">administrator</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">dataset_manager_role</AttributeValue>
          </Apply>
        </Apply>
      </Apply>
    </Condition>

Deny Access Functions
---------------------

Access to objects and their assorted binaries is described in our XACML policies in the :code:`Rule[@RuleId="deny-access-functions"][@Effect="Deny"]`
node. The node lists  the actions related to accessing content and disallows users to perform these without an exception.
While these nodes include all the functions (aka actions) a user should not be able to perform unless they are excepted in the
:code:`Rule[@RuleId="deny-access-functions"][@Effect="Deny"]/Condition[@FunctionId="urn:oasis:names:tc:xacml:1.0:function:not"]`
node, the actions section :code:`Rule[@RuleId="deny-access-functions"][@Effect="Deny"]/Target` is not relevant
for migration.  This is because the section is meant to be exhaustive and intends to include all actions associated with
accessing an object or its associated binaries.

Relevant to migration is the :code:`Rule[@RuleId="deny-access-functions"][@Effect="Deny"]/Condition[@FunctionId="urn:oasis:names:tc:xacml:1.0:function:not"]`
node.  This node includes the roles and users that are allowed to perform access actions and is separated into two
separate :code:`Apply[@FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of"]` sections.

.. code-block:: xml
    :caption: Deny Access Functions Exceptions

    <Condition FunctionId="urn:oasis:names:tc:xacml:1.0:function:not">
      <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:or">
        <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
          <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="urn:fedora:names:fedora:2.1:subject:loginId"/>
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">admin</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">ceaker</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">mbagget1</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">fedoraAdmin</AttributeValue>
          </Apply>
        </Apply>
        <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
          <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="fedoraRole"/>
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">administrator</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">dataset_manager_role</AttributeValue>
          </Apply>
        </Apply>
      </Apply>
    </Condition>

The first section describes the users that are allowed to perform access functions.  This rule is here as a precaution and
isn't important for migration.  By default, two system accounts are added here automatically plus the account of the
person who deposits the object originally and the dataset manager.

.. code-block:: xml
    :caption: Deny Access Functions - User Exceptions
    :emphasize-lines: 3-11

    <Condition FunctionId="urn:oasis:names:tc:xacml:1.0:function:not">
      <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:or">
        <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
          <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="urn:fedora:names:fedora:2.1:subject:loginId"/>
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">admin</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">ceaker</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">mbagget1</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">fedoraAdmin</AttributeValue>
          </Apply>
        </Apply>
        <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
          <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="fedoraRole"/>
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">administrator</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">dataset_manager_role</AttributeValue>
          </Apply>
        </Apply>
      </Apply>
    </Condition>

The second section is relevant for migration and describes the roles that should be able to access the object.

.. code-block:: xml
    :caption: Deny Access Functions - Role Exceptions
    :emphasize-lines: 12-18

    <Condition FunctionId="urn:oasis:names:tc:xacml:1.0:function:not">
      <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:or">
        <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
          <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="urn:fedora:names:fedora:2.1:subject:loginId"/>
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">admin</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">ceaker</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">mbagget1</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">fedoraAdmin</AttributeValue>
          </Apply>
        </Apply>
        <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
          <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="fedoraRole"/>
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">administrator</AttributeValue>
            <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">dataset_manager_role</AttributeValue>
          </Apply>
        </Apply>
      </Apply>
    </Condition>

Full XACML POLICY Example
-------------------------

Here is an example of a full :code:`POLICY` binary with multiple functions.

.. code-block:: xml
    :caption: XACML Policy Example


    <?xml version="1.0" encoding="UTF-8"?>
    <Policy xmlns="urn:oasis:names:tc:xacml:1.0:policy" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" PolicyId="islandora-xacml-editor-v1" RuleCombiningAlgId="urn:oasis:names:tc:xacml:1.0:rule-combining-algorithm:first-applicable">
      <Target>
        <Subjects>
          <AnySubject/>
        </Subjects>
        <Resources>
          <AnyResource/>
        </Resources>
        <Actions>
          <AnyAction/>
        </Actions>
      </Target>
      <Rule RuleId="deny-management-functions" Effect="Deny">
        <Target>
          <Subjects>
            <AnySubject/>
          </Subjects>
          <Resources>
            <AnyResource/>
          </Resources>
          <Actions>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-addDatastream</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-addDisseminator</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-adminPing</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-getDisseminatorHistory</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-getNextPid</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-ingest</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-modifyDatastreamByReference</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-modifyDatastreamByValue</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-modifyDisseminator</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-modifyObject</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-purgeObject</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-purgeDatastream</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-purgeDisseminator</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-setDatastreamState</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-setDisseminatorState</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-setDatastreamVersionable</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-compareDatastreamChecksum</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-serverShutdown</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-serverStatus</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-upload</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-dsstate</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-resolveDatastream</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-reloadPolicies</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
          </Actions>
        </Target>
        <Condition FunctionId="urn:oasis:names:tc:xacml:1.0:function:not">
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:or">
            <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
              <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="urn:fedora:names:fedora:2.1:subject:loginId"/>
              <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">admin</AttributeValue>
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">ceaker</AttributeValue>
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">mbagget1</AttributeValue>
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">fedoraAdmin</AttributeValue>
              </Apply>
            </Apply>
            <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
              <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="fedoraRole"/>
              <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">administrator</AttributeValue>
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">dataset_manager_role</AttributeValue>
              </Apply>
            </Apply>
          </Apply>
        </Condition>
      </Rule>
      <Rule RuleId="deny-access-functions" Effect="Deny">
        <Target>
          <Subjects>
            <AnySubject/>
          </Subjects>
          <Resources>
            <AnyResource/>
          </Resources>
          <Actions>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:api-a</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:api" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-getDatastreamHistory</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
            <Action>
              <ActionMatch MatchId="urn:oasis:names:tc:xacml:1.0:function:string-equal">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">urn:fedora:names:fedora:2.1:action:id-listObjectInResourceIndexResults</AttributeValue>
                <ActionAttributeDesignator AttributeId="urn:fedora:names:fedora:2.1:action:id" DataType="http://www.w3.org/2001/XMLSchema#string"/>
              </ActionMatch>
            </Action>
          </Actions>
        </Target>
        <Condition FunctionId="urn:oasis:names:tc:xacml:1.0:function:not">
          <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:or">
            <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
              <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="urn:fedora:names:fedora:2.1:subject:loginId"/>
              <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">admin</AttributeValue>
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">ceaker</AttributeValue>
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">mbagget1</AttributeValue>
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">fedoraAdmin</AttributeValue>
              </Apply>
            </Apply>
            <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-at-least-one-member-of">
              <SubjectAttributeDesignator DataType="http://www.w3.org/2001/XMLSchema#string" MustBePresent="false" AttributeId="fedoraRole"/>
              <Apply FunctionId="urn:oasis:names:tc:xacml:1.0:function:string-bag">
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">administrator</AttributeValue>
                <AttributeValue DataType="http://www.w3.org/2001/XMLSchema#string">dataset_manager_role</AttributeValue>
              </Apply>
            </Apply>
          </Apply>
        </Condition>
      </Rule>
      <Rule RuleId="allow-everything-else" Effect="Permit">
        <Target>
          <Subjects>
            <AnySubject/>
          </Subjects>
          <Resources>
            <AnyResource/>
          </Resources>
          <Actions>
            <AnyAction/>
          </Actions>
        </Target>
      </Rule>
    </Policy>

