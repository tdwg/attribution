
## Use Case: Creation of metadata after the fact and repairing metadata

**Point of Contact:** Sarah Ramdeen

**Use Case Name:** Metadata Later

**Goal**

To continue to improve the metadata of an object (physical or digital) after the initial collecting event or digitization event. The person who improved the metadata and how and when the improvement was made should be recorded. Any user should be able to find this information and use it to assess the actor.

**Summary**

Sarah is a metadata curator at a museum. She has found a mineral specimen that has the latitude and longitude inverted on the specimen card. She wants to fix this error in the electronic system the museum uses for managing specimens. Her department gets funding based on how much work they do, so the system needs to record who did the correction, when, and why.

**Actors**
* Metadata Curator, Sarah

**Preconditions**
* There already exists a system that contains a digital object (could be a digital representation of a physical object)
* The metadata curator logs in and finds the object and metadata of interest.
* Sarah has an ORCID
* A system of specimen identifiers is in place, such as IGSN
* A system of digital identifiers is in place, such as DOI or UUID  for digital objects in the collection.

**Post Conditions**
* Behind the scenes, the system records the correction, the reason/evidence for the correction, the identity of the curator, and the date/time of the correction. The previous incorrect data are also kept, but deprecated.
* Sarah is returned to the splash page for the digital object she was curating. There is a visual evidence that the change was made.
* Outsiders viewing the record should be able to see that changes have been made and when they were made.

**Triggers**
* The user locates incorrect data and clicks “edit” to make the correction

**Normal Flow**
* Sarah is presented with an editable version of the the incorrect data. 
* She makes the correction. Hits “ok”.
* The editable version of the data disappears
* She is prompted for the reason for the correction and any related evidence (possibly a controlled vocabulary)
* She adds the reason for the correction. Sarah uploads related documentation if relevant then hits “ok”

**Alternate Flows**
* Every “ok” or “edit” button should also be accompanied by a “cancel” button that takes the user back to the previous page (likely the digital object splash page)

**Exception Flows**
* If no evidence or reasoning is given for the change, the system should remind the user that this information is required and give another chance to add the information.  It may also prompt them to select a reason from a controlled vocabulary list.

**Entities**
* Agent - Sarah
* Action - In this case correcting inverted numbers
* Entity - latitude/longitude pair in the specimen metadata record
* Reason  - Sarah notices that the lat/long did not match the hemispheres of the locality
* DateTime of the Action

**Properties**
* wasGeneratedBy
* wasAssociatedWith
* hasAttribute

**Assertions**
* MetadataRecord wasGeneratedBy Correction
* Correction wasAssociatedWith Sarah
* Correction hasAttribute DateTime
* Correction hasAttribute Reason (added as comment)

**Entities and Properties to Add**
* Data Correction as subClass of Activity in VIVO
* Metadata Record as subClass of Entity in VIVO

**Example Query**
* What did Sarah do this year?
* How has this metadata record changed? PROVENANCE OUT OF SCOPE
* Who has changed this metadata record and why? We can’t answer the reason why easily because the Reason is added as a comment.
* Searching from a controlled vocabulary list of types of record changes, what was the most common change type?  Search for a specific type of error.
* Has this metadata record been changed?

**Notes**

The information should be changed by the curator, but there should also be a mechanism for reporting error by the end user to the curator or manager of the system. 
The data quality interest group in TDWG is working on defining a list of corrections that can be used as a controlled vocabulary for Activity

## Use Case: Curation of digital objects (video, audio, or images)

**Point of Contact:** Wim Hugo

**Use Case Name:** Digital Objects

**Goal** 

Keep track of a digital object and any processing that has been performed upon it. The processors should be able to get credit for adding value to the digital object.

**Summary**

Kenji is an academic oceanographer who is publishing a paper about primary productivity in the open ocean. He performed analyses on several publicly-available satellite images in order to improve resolution so he could use them in his paper. The improved images were then resubmitted back to the original repository. Maria, the data manager at this repository (of satellite images) notices that these two images are related to each other and wants other users to easily find this out and know that Kenji did the work. She wants to link the images in her repository and add metadata describing who did what to the original image that resulted in the improved image. 

**Actors**
* Kenji, oceanographer
* Maria, data manager

**Preconditions**
* There already exists a system that contains a digital object
* The data manager logs in and finds the object and metadata of interest.
* All actors have an ORCID
* A system of persistent, unique, dereferenceable IDs for digital objects is in place, like DOI
* The repository system is capable of generating citable references for users to copy into their publications for each digital object.

**Post Conditions**
* A citation is available for users that gives credit to Kenji for the analysis and the repository for stewardship, and enables the unambiguous identification of the image in question by a third party

**Triggers**
* Maria notices the two related images that are not formally connected in her repository
* She finds the splash page for the derived image
* Maria clicks on a button that says “Make Connection”. 

**Normal Flow**
* A pop up window appears with the ID and a thumbnail of the derived image on the left. Moving right there is an arrow pointing to the right and then a text box with two buttons underneath, “Connect” and “Cancel”
* Maria begins typing the ID of the original image in the text box and it is autofilled
* Maria clicks “Connect”
* The ID and a thumbnail of the original image appears on the right. A drop down list appears underneath the arrow.
* From this dropdown list, Maria chooses the relationship “derivedFrom”
* Two buttons appear, “OK” and “Cancel”
* Maria clicks “OK”
* The first popup disappears and a second appears asking for metadata about the relationship she just added
* The exact configuration of the metadata window depends on the relationship chosen previously. For DerivedFrom, the system asks for an actor(s), which is added via ORCID, the action from a controlled vocabulary, and a reference which in this case would be the doi of Kenji’s paper. The system would autoload the date and time of the upload of the derived image, but would allow Maria to edit. 
* There are two buttons at the bottom “OK” and “Cancel”. Maria clicks “OK”
* She is presented with a pop up review screen and clicks “Confirm” (there is also an “Edit” button)
* The system automatically adds that Maria is the one who created the “DerivedFrom” relationship on that day.

**Alternate Flows**
* Maria can click “Cancel” in any of the windows and the pop up disappears
* Clicking “Edit” in the final review screen will take the user to a single popup where everything is editable with an “OK” and a “Cancel” button. If the user hits “OK” the review screen reappears with the changes. If the user hits “Cancel” the pop up disappears and no changes are made.

**Exception Flows**
* If any of the boxes are left blank, when the user clicks “OK”, the system should remind the user that all information is required and then take him/her back to the editing window.

**Entities**
* Agent - In this case Maria
* Activity 1 - In this case connecting two related digital images
* Entity - In this case the digital images.
* Agent - In this case Kenji
* Activity 2 - In this case the modification of one image into another by Kenji
* Publication - In this case the paper Kenji published using the derived image

**Properties**
* wasGeneratedBy
* wasAssociatedWith
* hasAttribute

**Assertions**
* EnhancedImage wasGeneratedBy ModificationAction
* ModificationAction wasAssociatedWith Kenji
* ModificationAction hasAttribute DateTime
* Relationship wasGeneratedBy ConnectionActivity
* ConnectionActivity wasAssociatedWith Maria
* ConnectionActivity hasAttribute DateTime

**Entities and Properties to Add**
* Digital Object as subClass of Entity in VIVO
* Making a Connection or Adding a Relationship as subClass of Activity in VIVO

**Example Query**
* Who did the processing to create this image?
* Was this image derived from another image? OUT OF SCOPE
* How has Maria improved this database?
* Was anything published about this image or any derivative of this image? OUT OF SCOPE

**Notes**

Linking the digital images to the publication and to each other are out of scope for this use case. Attributing the creation of the derivedFrom relationship is in scope, but not the actual derivedFrom relationship.
View the recommendations from ICSU-WDS & RDA Publishing Data Services WG to link the image and the data set to the publication

## Use Case: Performance and collections review

**Point of Contact:** Jason and Vince

**Use Case Name:** Performance Review

**Goal**

Make the impact of curatorial activities quantitative for the purpose of curatorial staff performance review and assessing the resources needed to curate a collection

**Summary**

Ben is a collections manager in a natural history museum. He has a staff of five curators whose performance he must review annually. He has his own performance reviewed by a superior who is particularly interested in the overall state of the collections he oversees. He knows he doesn’t have enough staff to quickly curate all of the collections in the museum, so there is much curatorial work to be done that Ben thinks is important for his own review. Unfortunately, the only metric widely available for review is publication record. While publications are important, Ben wants his curators to feel comfortable spending time on curation activities instead of only publications. He would like to keep track of the curation activities of his employees and generate a “curation metric” that can be used in a review or on a CV. Sergey, one of the curators, has spent all year sorting and identifying (including DNA barcoding, entering each specimen into the museum’s specimen management software, and placing each specimen in its own container with a new label) small specimens in a large jar that were collected during a remote expedition over 100 years ago. He discovered a new species and was able to publish it, but Ben would like Sergey’s performance evaluation to reflect the large and important task of sorting through the entire jar, not just publishing the one new species. During his own performance review, he would like to be able to ask for the resources he needs to properly maintain the collections he oversees and have data to back up that request.

**Actors**
* Ben, collections manager
* Sergey, curator

**Preconditions**
* The museum uses specimen management software that powers an online portal where third parties can search for specimens the museum holds
* Sergey has logged in to this system during the course of his work and logged his activities
* All actors have an ORCID (ISNI - dead people)
* Every specimen in the system has a persistent, unique, and dereferenceable ID, such as IGSN
* Ben logs in to museum specimen management software as a manager

**Post Conditions**
* When Ben is done reviewing his curators’ work, he can exit the system and log out.

**Triggers**
* He can see a menu item “Review” under which he chooses “curators”

**Normal Flow**
* Ben is given the option to search or browse the curators in the system. The best option will depend on how many curators are present
* Ben chooses the curator of interest by clicking on the person’s name.
* Ben can see a high level summary of the person’s curatorial activities
* Ben can click through to see a more detailed version of the person’s curatorial activities

**Alternate Flows**
* Under the “Review” menu item, Ben can choose “specimens” instead of “curators”
* Ben is given the option to search or browse the specimens in the system. The best option will depend on how many specimens are present
* Ben chooses the specimen of interest by clicking on its ID. Metadata about the specimen are present to help Ben find the specimen he is looking for.
* Ben is shown a high level summary of how much the specimen is used

**Exception Flows**
* If Ben searches for something that isn’t present, he is presented with a message saying “no results”. The search box is still available for him to try again.

**Entities**
* Agent - Sergey
* Activity - a variety of specific curatorial tasks
* Entity - specimens
* DateTime - 

**Properties**
* wasGeneratedBy
* wasAssociatedWith
* hasAttribute

**Assertions**
* SpecimenB wasGeneratedBy SortingAction
* SortingAction wasAssociatedWith Sergey
* SortingAction hasAttribute DateTime
* SpecimenBTaxonID wasGeneratedBy IdentificationAction
* IdentificationAction wasAssociatedWith Sergey
* IdentificationAction hasAttribute DateTime
* SpecimenBBarCode wasGeneratedBy DNABarcodingAction
* DNABarcodingAction wasAssociatedWith Sergey
* DNABarcodingAction hasAttribute DateTime
* SpecimenBDigitalRecord wasGeneratedBy DigitizationAction
* DigitizationAction was AssociatedWith Sergey
* DigitizationAction hasAttribute DateTime
* SpecimenBMetadataRecord wasGeneratedBy MetadataGenerationAction
* MetadataGenerationAction wasAssociatedWith Sergey
* MetadataGenerationAction hasAttribute DateTime

**Entities and Properties to Add**
* Digitization as subClass of Activity in VIVO
* Physical Specimen as subClass of Entity in VIVO
* Look at taxonomic activities to add to VIVO as subClasses of Activity (Sorting, Identifying (Applying a name), barcoding, creating a digital record)

**Example Query**
* What did Sergey do in the collections last year?
* Who created this metadata label?
* Was this specimen separated out of a larger sample? Which one? OUT OF SCOPE
* How many large samples were subdivided into individual specimens last year?

**Notes**

This use case would also cover a museum or institution that wanted to measure its impact. They would query for their specimens and/or their researchers.

The association of the sorted specimens with the jar is out of scope, but is important. As is the link to the publication. Look to BCO to make axioms about the original collection of the “jar sample” and its subdivision. Consider the BCO process classes for the Activity.

## Use Case: Linking samples/specimens to other things that are related to them

**Point of Contact:** Sean and Sarah and Denise

**Use Case Name:** Analysis attribution

**Goal**

Make it easy to find data and research products related to a specimen/sample and keep track of a specimen/sample’s history and impact.

**Summary**

Victoria studies the history of climate change on Earth. An important source of data for her are sediment cores collected from old lakes. Many of these cores are stored in a special facility. They are expensive to collect and preserve and many analyses require destruction of a small part of the core. Thus, it is very important to be efficient with analyses. Victoria needs data from a specific lake to finish her work and has found a few publications about cores from that lake. She is able to find a core in the storage facility that would have the information she needs, but it is difficult to tell what kind of analyses have been run on it already, if any. She can’t be sure if this is the core that is discussed in the publications she found. Victoria would like to be able to discover information about the core through the storage facility website and add her contribution to the analysis for others to find. 

**Actors**
* Victoria, scientist

**Preconditions**
* There is a core storage facility that is searchable online. All the cores have a unique identifier, IGSN or similar.
* Victoria has an ORCID
* Victoria has searched the core facility and found a core she is interested in
* Various organizations related to the core have unique identifiers (funding institution like NSF, project which collected the cores, instrument used to collect the cores, etc.)
* Victoria is on the splash page for that core
* Listed on the splash page are publications (or supplemental information) which cite the core and they include a DOI (or other identifier)

**Post Conditions**
* Once Victoria has seen the metadata and analytical history of the core, she can trigger an action (clicking?) to request use of the core 
* If Victoria requests use of the core a message is sent to the core facility. If the request is granted evidence is visible in the analytical history of the core.
* After Victoria has analyzed the core, she returns to the splash for the core to report her analysis, DOIs for publications, or other results. A curator will be notified of the addition to approve it before it is added to the record.

**Triggers**
* Triggers an action (clicking?) to view the entire analytical history of the core

**Normal Flow**
* Victoria sees that there have been three analyses performed on parts of this core and two of those were included in a publication.
* Victoria clicks on each analysis to see the specific metadata for each. This includes the people involved, the methods, the funding agency, and any publications or other data products.
* She sees that one analysis she needs has not been performed on this core
* She requests use of the core from the storage facility. This process proceeds in accordance with the facility’s policies.
* After her analysis is done, she goes back to the splash page for the core and clicks on a button to add information. A pop-up form appears for her to add information about the analysis and any products.

**Alternate Flows**
* The core Victoria inspects is not what she needs. She clicks on a button to go back to search
* The analysis Victoria needs was already done.  She clicks on a button and downloads the analysis.  Victoria incorporates the analysis into her work, which results in a journal publication.  She returns to the core landing page to add her information ( publication citation and DOI) so that future searchers can find her work.

**Exception Flows**
* TBD

**Entities**
* Agent(s) - In this case Victoria and any other researcher that has analyzed the core
* Entity - Core
* Activity - Analysis
* DateTime

**Properties**
* wasGeneratedBy
* wasAssociatedWith
* hasAttribute

**Assertions**
* Data1 wasGeneratedBy Analysis1
* Analysis1 wasAssociatedWith Scientist1
* Analysis1 hasAttribute DateTime

**Entities and Properties to Add**
* Analysis as subClass of Activity in VIVO (any activity that generates data?)

**Example Query**
* What analyses have been performed on this core? OUT OF SCOPE
* What analyses have Victoria performed?
* Who has analyzed this core?
* Which data did Victoria create?

**Notes**

Linking the core, analysis, data, and publication is out of scope, but very important.
Look to IGSN to define links between physical specimens and publications or analyses. This can be done through the relatedIdentifier field in the IGSN metadata.

## Use Case: citizen science, students contribution

**Point of Contact:** 

**Use Case Name:** Citizen Science

**Goal**

Citizen scientists and volunteers can get credit for their contributions

**Summary**

Gretta is a volunteer at the Illinois Butterfly Monitoring Network. Once a month she records observations of butterflies along a transect using the Pollard Walk method. After she finishes her transect she adds her handwritten observations to an online system. After 10 years of volunteering she would like to compile a list of all the butterflies she has seen during the project.

**Actors**
* Gretta

**Preconditions**
* IBMN has an online system for recording their volunteers’ observations
* Each volunteer has an ORCID
* The IBMN system has identifiers for observations

**Post Conditions**
* TBD

**Triggers**
* TBD

**Normal Flow**
* TBD

**Alternate Flows**
* TBD

**Exception Flows**
* TBD

**Entities**
* Agent - Gretta
* Entity - Observation Record
* Action - Recording the observation

**Properties**
* wasGeneratedBy
* wasAssociatedWith
* hasAttribute

**Assertions**
* ObservationRecord wasGeneratedBy RecordingTheObservation
* RecordingTheObservation wasAssociatedWith Gretta
* RecordingTheObservation hasAttribute DateTime

**Entities and Properties To Add**
* TBD

**Example Query**
* How many butterfly species has Gretta seen?
* Who recorded this observation?
* How many observations did Gretta make last year?
* Which volunteer has seen the most monarch butterflies?
* Who saw the most butterflies in June of 2008?

**Notes**

The RecordingTheObservation Activity in this use case is referring to making the actual observation in the field, not to adding the observation to the online system. If the system needs to keep track of spotters, recorders, and the person who put the observation in the database after the fact, then more specific Activity types are needed.
Many contributors want to know the impact of their work. This implies a link to a publication or data set, which is out of scope.

## Use Case: Monitor professional contribution

**Point of Contact:** Jon Norenburg

**Use Case Name:** Professional Taxonomy

**Goal**

Professional taxonomist wants to keep track of the impact his specimens have on science

**Summary**

Joe is an invertebrate taxonomist at a natural history museum. He has spent decades collecting specimens and publishing new and revised taxa. The current system of professional rewards requires metrics that describe his contribution to science, including publication records. Joe has a page in ImpactStory that displays the impact of his publications, but nothing about his specimens. He knows that other taxonomists have viewed his collections on multiple occasions, but is not sure how his specimens have been used.

**Actors**
* Joe, a taxonomist

**Preconditions**
* Joe has an ORCID
* A system of unique, persistent, dereferenceable identifiers for specimens is in place

**Post Conditions**
* A JSON output is available for use by ImpactStory

**Triggers**
* TBD

**Normal Flow**
* TBD

**Alternate Flows**
* TBD

**Exception Flows**
* TBD

**Entities**
* Agent - Joe
* Entity - Specimens
* Publications
* Other Taxonomists
* Taxa

**Properties**
* wasGeneratedBy
* wasAssociatedWith
* hasAttribute

**Assertions**
* SpecimenA wasGeneratedBy CollectingActivity
* CollectingActivity wasAssociatedWith Joe
* CollectingActivity hasAttribute DateTime
* SpecimenATaxonID wasGeneratedBy IdentificationActivity
* IdentificationActivity wasAssociatedWith Joe
* IdentificationActivity hasAttribute DateTime
* Taxon1Revision was GeneratedBy RevisionActivity
* RevisionActivity wasAssociatedWith Scientist2
* RevisionActivity hasAttribute StartDate
* RevisionActivity hasAttrribute EndDate
* Data2 wasGeneratedBy Analysis2
* Analysis2 wasAssociatedWith Scientist3
* Analysis2 hasAttribute DateTime

**Entities and Properties to Add**
* Need to think about all the different taxonomic actions and add them to VIVO (Collection, Identification, Revision)
* Analysis as subClass of Activity in VIVO

**Example Query**
* Who used my specimen in a publication? OUT OF SCOPE
* Have data been generated from my specimen? By whom?
* How many specimens did Joe collect last year?

**Notes**

This use case would also cover a museum or institution that wanted to measure its impact. The would query for their specimens and/or their researchers.

The first assertion should probably be handled by BCO partly. IGSN uses its own “collector” field.

Associations with publications or data are out of scope, but important. IGSN can accommodate links to publications and data via relatedIdentifier, which is a DOI.

## Use Case: Mass curatorial actions on databases

**Point of Contact:** Vince Smith

**Use Case Name:** Mass actions on databases

**Goal**

Maintain the provenance and attribution of curatorial actions on whole databases

**Summary**

Sophie is a database manager at a museum. She is regularly given large data files by the scientists who work at the museum for upload into the database. These files often require a high degree of manipulation before they can be uploaded. She is also responsible for guaranteeing the quality and availability of the database. That means she needs to run error-finding algorithms and occasionally needs to update the database software. These processes are important and need to be attributed to her.

**Actors**
* Sophie, database manager

**Preconditions*
* TBD

**Post Conditions**
* TBD

**Triggers**
* TBD

**Normal Flow**
* TBD

**Alternate Flows**
* TBD

**Exception Flows**
* TBD

**Entities**
* TBD

**Properties**
* TBD	

**Notes**

Identified as low priority at TDWG 2016

RDA P9 - worth including

## Use Case: Digitization

**Point of Contact:** Vince Smith

**Use Case Name:** Digitization

**Goal**

Keep track of which specimens were digitized by whom

**Summary**

Employ teams of people to digitize a physical collection and create records about objects. Scanning herbarium sheets. Photographing pinned insects. 3D scanning of fossils. They are the point of contact for applying the identifier i.e. adding the barcode. Especially for the legacy specimens. Transcribing information about specimens from specimen labels. 

**Actors**
* Digitizer

**Preconditions**
* TBD

**Post Conditions**
* TBD

**Triggers**
* TBD

**Normal Flow**
* TBD

**Alternate Flows**
* TBD

**Exception Flows**
* TBD

**Entities**
* Agent - Digitizer
* Entity - Physical Object Being Digitized
* Entity - Digital Object derived from physical object
* Activity - Digitization

**Properties**
* wasGeneratedBy
* wasAssociatedWith
* hasAttribute

**Assertion**
* DigitalObject wasGeneratedBy DigitizationActivity
* DigitizationActivity wasAssociatedWith Digitizer
* DigitizationActivity hasAttribute DateTime

**Entities and Properties to Add**
* Digitization as subClass of Activity in VIVO

**Example Query**
* How many specimens did Kay digitize in August?
* How many specimens have been digitized?
* Who digitized this specimen?
* When was this specimen digitized?

**Notes**

The digital object needs to be linked to the physical object, but that is out of scope. The IGSN metadata record can link a physical object to its digital representation via relatedIdentifier, if the digital representation has a DOI (recommended) or some other form of UUID.

Check with iDigBio to make sure this meets their needs.

## Use Case: Funder
**Point of Contact:** Alex (iDigBio)

**Use Case Name:** Funding Impact

**Goal**

Demonstrate the impact of research funding

**Summary**

Research funding agencies and foundations must show that they are spending money effectively and having an impact. The products of a research grant must be identifiable and their use must be documented. Martin is an intern at a foundation that funds collecting expeditions. He has been asked to work on the annual report to the board that demonstrates how their funds were used. Martin’s boss wants him to locate all the research products of a specific expedition and find all instances of those products contributing to the increase in scientific knowledge.

**Actors**
* Martin, intern

**Preconditions**
* TBD

**Post Conditions**
* TBD

**Triggers**
* TBD

**Normal Flow**
* TBD

**Alternate Flows**
* TBD

**Exception Flows**
* TBD

**Entities**
* Funder (Agency, organization, etc)
* Expedition
* Specimens collected during expedition
* Publications

**Properties**
* wasGeneratedBy
* wasAssociatedWith
* hasAttribute

**Assertions**
* TBD

**Notes**
Priority Low - out of scope - maybe rewrite

Look to VIVO for was to attribute research outputs to funding agencies. Maybe this is a use case for VIVO?

Look at the Professional Taxonomist use case.

## Use Case: Transforming a digital or physical object by creating a secondary object

**Point of Contact:** Sarah Ramdeen

**Use Case Name:** Object Transformation - secondary object

**Goal**

Keep track of the transformation of an object in a collection.

**Summary**

Ruth is curator for a collection of materials related to snow and ice.  One of the items in her collection is a scientific map.  She discussed the map with members of the indigenous community and they were able to give her additional information from their historical knowledge of the area.  She has the new information as an overlay - handwritten annotations on a copy of the map.  The transformed object needs to be added to the collection records with the connection  to the original documented.

**Actors**
* Ruth, curator of the collection

**Preconditions**
* The system allows for records to be connected with a defined relationship

**Post Conditions**
* TBD

**Triggers**
* Something changed with an item in the collection.  This may be the addition of annotations but includes such variations as re-housing samples which may result in a secondary related object which will need a record in the database

**Normal Flow**
* Ruth creates a new record for the annotations.  
* On the record screen, she selects the field that indicates this item relates to an existing item in the collection.
* A popup appears that asks Ruth to enter the unique ID for the existing item, and to define the relationship between the two items (perhaps from a controlled vocabulary).
* Both records are edited to demonstrate the relationship and record Ruth’s ORCID, and the date the relationship was created.

**Alternate Flows**
* TBD

**Exception Flows**
* TBD

**Entities**
* Person doing the transformation
* DateTime - Start time and end time? Transformations can take a while.
* Reason for the transformation
* Transformation action
* Primary Object (the map)
* Secondary Object (the overlay)
* Transformed Object (the map with the overlay)

**Properties**
* wasGeneratedBy
* wasAssociatedWith
* hasAttribute

**Assertion**
* TransformedObject wasGeneratedBy Transformation
* Transformation wasAssociatedWith Ruth
* Transformation hasAttribute StartTime
* Transformation hasAttribute EndTime
* secondaryObject wasGeneratedBy ResearchActivity
* ResearchActivity wasAssociatedWith Ruth
* ResearchActivity hasAttribute StartTime
* ResearchActivity hasAttribute EndTime

**Entities and Properties to Add**
* Transformation as subClass of Activity in VIVO

**Example Query**
* Who created this overlay?
* Has this map been transformed? When?

**Notes**

The map before the overlay must be connected to the map + the overlay, probably with PROV derivedFrom, but this is out of scope

## Use Case: Nomenclature Curation
**Point of Contact:** Nicky Nicholson

**Use Case Name:** Nomenclature

**Goal**

Give attribution for the maintenance and research of nomenclatural acts that support authoritative classifications

**Summary**

Sharon is a curator at an herbarium who works as part of a team to maintain an authoritative plant classification. This classification is used by many other institutions and projects as essential infrastructure. The impact of her work and the work of her team is huge, but no one knows that she is behind the scenes. This can be a problem when funding is up for renewal. How can Sharon really know her contribution and communicate that to her funder?

**Actors**
* Sharon, curator

**Preconditions**
* An authoritative plant classification is available and editable by a team of curators (e.g. IPNI)
* A system of identifiers is in place

**Post Conditions**
* TBD

**Triggers**
* TBD

**Normal Flow**
* TBD

**Alternate Flows**
* TBD

**Exception Flows**
* TBD

**Entities**
* Person doing the action, in this case Sharon
* Agent - museum supporting Sharon, maybe an additional funding agency
* Curatorial act
* DateTime
* Reason

**Properties**
* wasGeneratedBy
* wasAssociatedWith
* hasAttribute

**Assertions**
* AcceptedNameUsage wasGeneratedBy Analysis
* Analysis wasAssociatedWith Sharon
* Analysis hasAttribute DateTime
* Analysis hasAttribute Reason (justification for change, possibly a reference to a published nomenclatural act)

**Entities and Properties to Add**
* Think of all the ways a classification can be revised and add as subClasses of Activity in VIVO

**Example Query**
* How has Sharon improved this classification?
* Who made this nomenclatural assertion in our system?
* When was this name changed in our system?
* What did Sharon do yesterday?

**Notes**

If Sharon’s actions can be attributed to an institution or funder, then it should be, but this is out of scope. VIVO may be able to help here.

It might be best to add references in a different way than as a comment in hasAttribute

## Use Case: Transforming a digital or physical object by permanently changing the object
**Point of Contact:** Sarah Ramdeen

**Use Case Name:** Object Transformation - permanent change

**Goal**

Keep track of the transformation of an object in a collection.

**Summary**

Alex is a curator of a mammal collection. Some of their specimens are large taxidermied organisms that were collected a century ago. The specimens are showing their age and need to be restuffed. 

**Actors**
* Alex, curator of the collection

**Preconditions**
* A database exists with a unique identifier for each specimen
* Database has fields that can be filled into reflect changes/modifications such as restuffing.

**Post Conditions**
* The object is not changed so radically that it changes it scientific value.  Changes made to more accurately reflect knowledge of the specimen within reason.  If it does change the scientific value (or type of organism it represents), a new record should be created with a link to the past information/history of the change.	

**Triggers**
* Specimen is falling apart and may deteriorate over time if not fixed.

**Normal Flow**

Alex notices that one of the objects on display is deteriorating. He decides to fix the object.  When he removes it from the display case, he notes that the reason it looks off/is deteriorating is that the original materials used to preserve the specimen were not archival and are breaking down.  He has to remove a lot of the internal materials used to create the structure under the specimen.  He rebuilds the specimen with modern materials and it still appears the same from the outside.  He edits the record in the database to reflect this instance of change to the specimen in case there are questions in the future about the process, materials used, materials removed, etc.

**Alternate Flows**

During Alex’s rebuilding of the specimen, important parts are damaged and are unable to be rebuilt. The museum has another specimen in the collection from a similar age, same scientific specimen, but is a duplicate or planned to be de-acquisitioned, or otherwise replaceable. Alex uses pieces from this second specimen to combine with the first.  He edits the record in the database to reflect this process. This may result in the creation of a new specimen with a new museum specimen id.

**Exception Flows**

Alex begins to restructure the deteriorating specimen but it is too damaged and removing the deteriorating parts will destroy the specimen.  Alex notes this in the record and decides to maintain the specimen as-is without change.  He notes in the record that a new example should be acquired.

**Entities**
* Person doing the transformation
* DateTime - Start time and end time? Restuffing can take a while.
* Reason for the transformation
* Transformation action (restuffing)
* Entity being transformed (the mammal specimen)

**Properties**
* wasGeneratedBy
* wasAssociatedWith
* hasAttribute

**Assertion**
* TransformedObject wasGeneratedBy Transformation
* Transformation wasAssociatedWith Alex
* Transformation hasAttribute StartTime
* Transformation hasAttribute EndTime

**Entities and Properties to Add**
* Transformation as subClass of Activity in VIVO

**Example Query**
* Who restuffed this specimen?
* Has this item been transformed? When?

**Notes**

There was much discussion over the identity of the specimen pre and post stuffing. The museum specimen number is unlikely to change because of a restuffing or removal of a leg for molecular analysis; however it is easy to imagine scenarios where the specimen would be considered something new worthy of another identifier post transformation. In the case that the transformed specimen needs a new identifier, we recommend using the “derivedFrom” property in PROV to link the transformed object to the original object.

