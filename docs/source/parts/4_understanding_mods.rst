Understanding MODS
==================

MODS 3.5 is used for descriptive metadata for our datasets.  All datasets and their parts have its own descriptive
metadata section.  The original intention was that there would be use cases where the parts needed to have separate
descriptive metadata.  To date, this has never been leveraged and is not a  requirement in the future.

While metadata usage is inconsistent across the entire repository, datasets have the following metadata application
profile.

+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Field                      | Final Xpath                                          | Description                                        |
+============================+======================================================+====================================================+
| Title / Label              | /titleInfo/title                                     | The title or label of the dataset.                 |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Publication Date           | originInfo/dateIssued[@keyDate="yes"]                | The date of publication.                           |
|                            | [@encoding="edtf"]                                   |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Series Title               | relatedItem[@type="series"]/titleInfo/title          | The title of the series the datasets belong to.    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Submission Date            | recordInfo[@displayLabel="Submission"]               | The submission date of the object.                 |
|                            | /recordCreationDate[@encoding="w3cdtf"]              |                                                    |
|                            |                                                      |                                                    |
|                            | originInfo/dateCreated                               |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Identifier                 | identifier[@type="local"]                            | Any local identifiers.                             |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Depositor First/Given Name | name[role/roleTerm/text()="Depositor"]               | The given name of the depositor.                   |
|                            | /namePart[@type="given"]                             |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Depositor Last/Family Name | name[role/roleTerm/text()="Depositor"]               | The family name fo the depositor.                  |
|                            | /namePart[@type="family"]                            |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Depositor Suffix           | name[role/roleTerm/text()="Depositor"]               | The termOfAddress of the depositor.                |
|                            | /namePart[@type="termsOfAddress"]                    |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Depositor ORCid iD         | name[role/roleTerm/text()="Depositor"]               | The ORCiD identifier of the depositor if provided. |
|                            | /@vauleURI                                           |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Department 1               | name[role/roleTerm/text()="Depositor"]               | The primary department of the depositor.           |
|                            | /affiliation[1]                                      |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Department 2               | name[role/roleTerm/text()="Depositor"]               | The secondary department of the depositor.         |
|                            | /affiliation[2]                                      |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Center 1                   | name[role/roleTerm/text()="Depositor"]               | The primary center of the depositor.               |
|                            | /affiliation[3]                                      |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Center 2                   | name[role/roleTerm/text()="Depositor"]               | The secondary department of the depositor.         |
|                            | /affiliation[4]                                      |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| College                    | name[role/roleTerm/text()="Depositor"]               | The college associated with the depositor.         |
|                            | /affiliation[5]                                      |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| University                 | name[role/roleTerm/text()="Depositor"]               | The university associated with the depositor.      |
|                            | /affiliation[6]                                      |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Creator-n First/Given Name | name[role/roleTerm/text()="Creator"]                 | The given name of a creator.                       |
|                            | /namePart[@type="given"]                             |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Creator-n Last/Family Name | name[role/roleTerm/text()="Creator"]                 | The family name of the creator.                    |
|                            | /namePart[@type="family"]                            |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Creator-n Suffix           | name[role/roleTerm/text()="Creator"]                 | The termOfAddress of the creator.                  |
|                            | /namePart[@type="termsOfAddress"]                    |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Keywords                   | subject/topic                                        | The keywords associated with an object.            |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| "Genre"                    | physicalDescription/form[@authority="coar"]          | Genre terms related to object                      |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| "Type of Resource"         | typeOfResource                                       | Type of Resource                                   |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| ISNI Identifier            | recordInfo/recordContentSource[@authority="isni"]    | ISNI Identifier                                    |
|                            | /@valueURI                                           |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| ISNI Label                 | recordInfo/recordContentSource[@authority="isni"]    | ISNI Label                                         |
|                            | /text()                                              |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Related Article Title      | relatedItem[@displayLabel="Article"]/titleInfo/title | Title of a Related Article                         |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Related Article Location   | relatedItem[@displayLabel="Article"]/location/url    | URL of Related Article                             |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| Related Article Citation   | relatedItem[@displayLabel="Article"]                 | Citation to related article                        |
|                            | /note[@displayLabel="Citation"]                      |                                                    |
+----------------------------+------------------------------------------------------+----------------------------------------------------+
| DOI (Published Version)    | identifier[@type="doi"]                              | DOI of the dataset                                 |
+----------------------------+------------------------------------------------------+----------------------------------------------------+

Sample MODS record
------------------

A MODS record for an object looks similar to this:

.. code-block:: xml
    :caption: Sample MODS record

    <?xml version="1.0" encoding="UTF-8"?>
    <mods:mods xmlns:mods="http://www.loc.gov/mods/v3" xmlns="http://www.loc.gov/mods/v3" xmlns:etd="http://www.ndltd.org/standards/metadata/etdms/1.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xs="http://www.w3.org/2001/XMLSchema" xsi:schemaLocation="http://www.loc.gov/mods/v3 http://www.loc.gov/standards/mods/v3/mods-3-5.xsd" version="3.5">
      <mods:titleInfo>
        <mods:title>Data Fitness for Use - INTERVIEWS</mods:title>
      </mods:titleInfo>
      <mods:name valueURI="">
        <mods:namePart type="given">Bradley Wade</mods:namePart>
        <mods:namePart type="family">Bishop</mods:namePart>
        <mods:role>
          <mods:roleTerm authority="marcrelator" type="text" valueURI="http://id.loc.gov/vocabulary/relators/dpt">Depositor</mods:roleTerm>
        </mods:role>
        <mods:namePart type="termsOfAddress"/>
        <mods:affiliation/>
        <mods:affiliation/>
        <mods:affiliation/>
        <mods:affiliation/>
      </mods:name>
      <mods:name>
        <mods:namePart type="given">Bradley Wade</mods:namePart>
        <mods:role>
          <mods:roleTerm authority="marcrelator" type="text" valueURI="http://id.loc.gov/vocabulary/relators/cre">Creator</mods:roleTerm>
        </mods:role>
        <mods:namePart type="family">Bishop</mods:namePart>
        <mods:namePart type="termsOfAddress"/>
      </mods:name>
      <mods:abstract>This data set is restricted. Contact Wade Bishop (bbisho13@utk.edu) to request access to this data set. This study assesses science data reusers’ information-seeking behavior to determine fitness for use, a concept from consumer behavior research that explains how consumers define and assess product quality and compatibility to satisfy their specific needs. Using a critical incident technique, 22 researchers in earth science described their most recent data discovery resulting in reuse. An interview schedule derived from the FAIR Data Principles framed participants’ information seeking behavior along a sequence of actions, which included finding, accessing, making interoperable, and reusing data.</mods:abstract>
      <mods:subject>
        <mods:topic>Data Discovery</mods:topic>
      </mods:subject>
      <mods:subject>
        <mods:topic>Science</mods:topic>
      </mods:subject>
      <mods:subject>
        <mods:topic>Data Fitness for Use</mods:topic>
      </mods:subject>
      <mods:subject>
        <mods:topic>Critical Incident Technique</mods:topic>
      </mods:subject>
      <mods:physicalDescription>
        <mods:form authority="coar" valueURI="http://purl.org/coar/resource_type/c_ddb1">dataset</mods:form>
      </mods:physicalDescription>
      <mods:typeOfResource>software, multimedia</mods:typeOfResource>
      <mods:recordInfo>
        <mods:recordContentSource authority="isni" valueURI="http://www.isni.org/isni/0000000123151184">University of Tennessee (Knoxville)</mods:recordContentSource>
        <mods:languageOfCataloging>
          <mods:languageTerm type="code" authority="iso639-2b">eng</mods:languageTerm>
        </mods:languageOfCataloging>
        <mods:recordOrigin>Created and edited in general conformance to MODS Guidelines (Version 3.5).</mods:recordOrigin>
      </mods:recordInfo>
      <mods:relatedItem type="series">
        <mods:titleInfo>
          <mods:title>Faculty and Graduate Student Research and Creative Work</mods:title>
        </mods:titleInfo>
      </mods:relatedItem>
      <mods:relatedItem displayLabel="Article">
        <mods:titleInfo>
          <mods:title/>
        </mods:titleInfo>
        <mods:location>
          <mods:url/>
        </mods:location>
        <mods:note displayLabel="citation"/>
      </mods:relatedItem>
      <mods:relatedItem displayLabel="Funder">
        <mods:titleInfo type="alternative">
          <mods:title>US Dept. of Commerce</mods:title>
          <mods:subTitle/>
        </mods:titleInfo>
        <mods:identifier/>
      </mods:relatedItem>
      <mods:identifier type="doi">https://www.doi.org/10.7290/ai1y12d</mods:identifier>
      <mods:note type="preferred citation"/>
      <mods:originInfo>
        <mods:dateCaptured point="start">2017-10-02</mods:dateCaptured>
        <mods:dateCaptured point="end">2017-12-18</mods:dateCaptured>
      </mods:originInfo>
      <mods:typeOfResource>software, multimedia</mods:typeOfResource>
      <mods:recordInfo>
        <mods:recordContentSource authority="isni" valueURI="http://www.isni.org/isni/0000000123151184">University of Tennessee (Knoxville)</mods:recordContentSource>
        <mods:languageOfCataloging>
          <mods:languageTerm type="code" authority="iso639-2b">eng</mods:languageTerm>
        </mods:languageOfCataloging>
        <mods:recordOrigin>Created and edited in general conformance to MODS Guidelines (Version 3.5).</mods:recordOrigin>
      </mods:recordInfo>
      <mods:relatedItem type="series">
        <mods:titleInfo>
          <mods:title>Faculty and Graduate Student Research and Creative Work</mods:title>
        </mods:titleInfo>
      </mods:relatedItem>
      <mods:typeOfResource>software, multimedia</mods:typeOfResource>
      <mods:recordInfo>
        <mods:recordContentSource authority="isni" valueURI="http://www.isni.org/isni/0000000123151184">University of Tennessee (Knoxville)</mods:recordContentSource>
        <mods:languageOfCataloging>
          <mods:languageTerm type="code" authority="iso639-2b">eng</mods:languageTerm>
        </mods:languageOfCataloging>
        <mods:recordOrigin>Created and edited in general conformance to MODS Guidelines (Version 3.5).</mods:recordOrigin>
      </mods:recordInfo>
      <mods:relatedItem type="series">
        <mods:titleInfo>
          <mods:title>Faculty and Graduate Student Research and Creative Work</mods:title>
        </mods:titleInfo>
      </mods:relatedItem>
      <mods:typeOfResource>software, multimedia</mods:typeOfResource>
      <mods:recordInfo>
        <mods:recordContentSource authority="isni" valueURI="http://www.isni.org/isni/0000000123151184">University of Tennessee (Knoxville)</mods:recordContentSource>
        <mods:languageOfCataloging>
          <mods:languageTerm type="code" authority="iso639-2b">eng</mods:languageTerm>
        </mods:languageOfCataloging>
        <mods:recordOrigin>Created and edited in general conformance to MODS Guidelines (Version 3.5).</mods:recordOrigin>
      </mods:recordInfo>
      <mods:relatedItem type="series">
        <mods:titleInfo>
          <mods:title>Faculty and Graduate Student Research and Creative Work</mods:title>
        </mods:titleInfo>
      </mods:relatedItem>
      <mods:typeOfResource>software, multimedia</mods:typeOfResource>
      <mods:recordInfo>
        <mods:recordContentSource authority="isni" valueURI="http://www.isni.org/isni/0000000123151184">University of Tennessee (Knoxville)</mods:recordContentSource>
        <mods:languageOfCataloging>
          <mods:languageTerm type="code" authority="iso639-2b">eng</mods:languageTerm>
        </mods:languageOfCataloging>
        <mods:recordOrigin>Created and edited in general conformance to MODS Guidelines (Version 3.5).</mods:recordOrigin>
      </mods:recordInfo>
      <mods:relatedItem type="series">
        <mods:titleInfo>
          <mods:title>Faculty and Graduate Student Research and Creative Work</mods:title>
        </mods:titleInfo>
      </mods:relatedItem>
      <mods:typeOfResource>software, multimedia</mods:typeOfResource>
      <mods:recordInfo>
        <mods:recordContentSource authority="isni" valueURI="http://www.isni.org/isni/0000000123151184">University of Tennessee (Knoxville)</mods:recordContentSource>
        <mods:languageOfCataloging>
          <mods:languageTerm type="code" authority="iso639-2b">eng</mods:languageTerm>
        </mods:languageOfCataloging>
        <mods:recordOrigin>Created and edited in general conformance to MODS Guidelines (Version 3.5).</mods:recordOrigin>
      </mods:recordInfo>
      <mods:relatedItem type="series">
        <mods:titleInfo>
          <mods:title>Faculty and Graduate Student Research and Creative Work</mods:title>
        </mods:titleInfo>
      </mods:relatedItem>
      <mods:typeOfResource>software, multimedia</mods:typeOfResource>
      <mods:recordInfo>
        <mods:recordContentSource authority="isni" valueURI="http://www.isni.org/isni/0000000123151184">University of Tennessee (Knoxville)</mods:recordContentSource>
        <mods:languageOfCataloging>
          <mods:languageTerm type="code" authority="iso639-2b">eng</mods:languageTerm>
        </mods:languageOfCataloging>
        <mods:recordOrigin>Created and edited in general conformance to MODS Guidelines (Version 3.5).</mods:recordOrigin>
      </mods:recordInfo>
      <mods:relatedItem type="series">
        <mods:titleInfo>
          <mods:title>Faculty and Graduate Student Research and Creative Work</mods:title>
        </mods:titleInfo>
      </mods:relatedItem>
    </mods:mods>