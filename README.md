# Ambient Book Shopping - Intelligent Book Retail Experience
- This project is developed by *Natnael Berhanu Takele*
- Student Id: *s5446838*

## Repository Organization

In this repository, you'll find the ontology file named "Ambient_Book_Shopping_Ontology.Owl," along with the README.md file. To utilize the ontology, simply open it with Protègè 5.5.

## Project Overview

Welcome to Ambient Book Shopping, an innovative project designed to create a smart environment for a seamless and enjoyable book-buying experience. The traditional challenges faced in libraries, such as time-consuming searches for favorite books, lengthy checkout processes, and inadequate surveillance, are addressed through this project.

### Key Solutions:

1. **Preference-Based Navigation:**
   - Implemented through a stereo camera, the system captures customer images, processes data, and recommends specific rooms based on preferences.
   - Customers can select their desired section on a screen near the entrance, and the system guides them directly to the chosen location.

2. **Efficient Book Purchase:**
   - Book purchases are simplified by allowing customers to scan book barcodes using their mobile phones.
   - The barcode integrates an RFID antenna, enabling quick and secure transactions.

3. **Enhanced Security:**
   - The stereo camera serves as a surveillance tool, detecting any suspicious activities, especially book theft.
   - Bookcases are equipped with box that can only be opened by a switch, minimizing the risk of theft, vandalism, or misplaced books.


### Ontology Knowledge Representation

The Ambient Book Shopping ontology is created using Protègè and the Pellet reasoner, adhering to the following guidelines:

- **Top Classes (TBox):**
  - At least 3 top classes are defined.
  - 7 top classes are introduced, including Engagement, Book, Box, Persona, Section, Sensor, and Bookcase.

- **Object Properties (TBox):**
  - At least 4 object properties are established.
  - 13 object properties are created, facilitating relationships between classes.

- **Data Properties (TBox):**
  - 7 data properties are defined, enhancing the ontology with additional details.
 
### TBOX

#### Classes and Sub-classes

1. Engagement: Represents actions in the shop, identified by overlapping with sensors. (Engagement = ∃overlap.Sensor)

    - PurchaseBookEngagement: is a sub class of engagement and it is activated when the mobile phone scans a barcode.
        (PurchaseBookEngagement = Engagement ⋂ ∃(overlap.RFIDAntennaSensor ⋂ overlap.MobilePhone).
    - AccessedEngagement: is a sub class of engagement and Overlaps with PIR or stereo camera sensors, indicating a person's entry.
        (AccessedEngagement = Engagement ⋂ ∀(overlap.CameraSensor ⋂ overlap.PIRSensor)
    - UnlockBoxEngagement: is a sub class of engagement and it is triggered when using the interrupt switch.
        (UnlockBookEngagement = Engagement ⋂ ∀overlap.SwitchSensor)
2. Book: Represents books for sale on Bookcases with barcodes and page numbers.
        (Book = ∃isBookof.BookCase ⋂ ∃hasPage.int ⋂ ∀hasSensor.RFIDAntennaSensor)

    - AdrenalineFilledBook: Books of adrenaline filled type placed on the RedBookCase class
        (AdrenalineFilledBook = Book ⋂ ∀isBookof.RedBookCase ...)
    - JourneyOfDiscoveryBook: Books of journey of discovery type placed on the BlueBookCase class
        (JourneyOfDiscoveryBook = Book ⋂ ∀isBookof.BlueBookCase ...)
    - CartoonBook: Books of cartoon placed on the OrangeBookCase class
        (CartoonBook = Book ⋂ ∀isBookof.OrangeBookCase ...)
    - MagicFilledBook: Books of magic filled type placed on the GreenBookCase class
        (MagicFilledBook= Book ⋂ ∀isBookof.GreenBookCase ...)
    - RomanceBook: Books of romantic type placed on the PinkBookCase class
        (RomanceBook= Book ⋂ ∀isBookof.PinkBookCase ...)
    - EasternComicBook: Books of eastern comic placed on the WhiteBookCase class
        (EasternComicBook= Book ⋂ ∀isBookof.WhiteBookCase ...)
    - SpiritualBook: Books of spiritual type placed on the BlackBookCase class
        (SpiritualBook= Book ⋂ ∀isBookof.BlackBookCase ...)
    - MetaPhysicalBook: Books of meta physical type placed on the YellowBookCase class
        (MetaPhysicalBook= Book ⋂ ∀isBookof.YellowBookCase ...)
      
3. Box: This class represents boxes covering book cases and doors with a switch sensor for opening.
        (Box = ∀hasSensor.SwitchSensor ⋂ ∃isBoxOf.BookCase ⋃ ∃isBoxOf.Section)

4. Persona: Represents customers who engage in activities, possess a mobile phone for barcode reading (a sub-class of a camera sensor), and tracks the number of books purchased.
        (Persona = ∃hasFinished.Engagement ⋂ ∃hasMobilePhone.MobilePhone ⋂ ∃hasPurchasedBook.integer)

5. Section: Represents shop sections (rooms) connected to one another, each having a specific number of book cases and a box.
        (Section = (∃hasBookCase.BookCase ⋃ ∃hasBox.Box) ⋂ ∃isLinked.Section ⋂ ∃hasBookCaseNumber.int

    - TerrifyingSection: Section that contains red book cases and blue ones, in a range of 2-5. It is linked to the entry room.
    - DesiredHavenSection: Section that contains green book cases with the value of 1. It is linked to the entry room.
    - EntrySection: Principal section that has no book cases and contains the PIR, stereo camera and switch sensors. It is connected to all sections and has a case (the door) to open if you want to buy a book.
    - RomanticSpiritualSection: Section that contains pink Book cases and black ones, in a range of 6-7. It is linked to the entry room.
    - ArtSection: Section that contains white book cases and orange ones, in a range of 8-9. It is linked to the entry room.
    - PhilosophySection: Section that contains yellow book cases with the value of 1. It is linked to the entry room.
      
6. Sensor: Represents sensors involved in the outlet, a primitive class with sub-classes.
    - CameraSensor: Camera sensor sub class that includes the stereo camera in the Entrance and mobile phone here considered as a sensor
          (CameraSensor = Sensor ⋂ ∀isSensorof.Room)
      - MobilePhone: is a sub-class of camera sensor that a person has
            (MobilePhone = CameraSensor ⋂ ∀isMobilePhoneOf.Persona)
      - StereoCameraSensor: is a sub-class of camera sensor stays in the Entrance
            (StereoCameraSensor = CameraSensor ⋂ ∀isSensorOf.EntrySection)
    - PIRSensor: PIR sensor positioned on the entrance of the shoop to determine if someone is entered or not
          (PIRSensor = Sensor ⋂ ∀isSensorof.EntranceRoom)
    - RFIDAntennaSensor: RFID implemented in books, so every sensor of this type has a bar code (key) associated
          (RFIDAntennaSensor = Sensor ⋂ ∀isSensorOf.Book ⋂ ∃hasKey.unsignedLong)
    - SwitchSensor: Switch sensor near boxes
          (SwitchSensor = Sensor ⋂ ∀isSensorOf.Box)
  
      
      
7. BookCase: Represents book cases containing books in various genres, associated with colors and cases. Counts the number of books on each book case.
          (BookCase = ∃hasBook.Book ⋂ ∃hasBox.Box ⋂ ∃inSection.Section ⋂ ∃hasBookNumber.(>=1) ⋂ ∃hasColor.string)

    - BlackBookCase: contains spiritual books and has black colors, and it is placed in the Romantic Spiritual Section
          (BlackBookCase = BookCase ⋂ ∃hasColor."Black" ⋂ ∃hasBook.SpiritualBook ⋂ ∀inSection.RomanticSpiritual ...)
    - BlueBookCase: contains journey of discovery books and has blue colors, and it is placed in the Terrifying section
          (BlueBookCase = BookCase ⋂ ∃hasColor."Blue" ⋂ ∃hasBook.JourneyOfDiscoveryBook ⋂ ∀inSection.TerrifyingSection ...)
    - GreenBookCase: contains magic filled books and has green colors, and it is placed in the Desired Haven section
          (GreenBookCase = BookCase ⋂ ∃hasColor."G" ⋂ ∃hasBook.MagicFilledBook ⋂ ∀inSection.DesiredHavenSection ...)
    - OrangeBookCase: contains cartoon books and has orange colors, and it is placed in the Art section
          (OrangeBookCase = BookCase ⋂ ∃hasColor."O" ⋂ ∃hasBook.CartoonBook ⋂ ∀inSection.ArtSection ...)
    - PinkBookCase: contains romance books and has pink colors, and it is placed in the Romantic Spiritual Section
          (PinkBookCase = BookCase ⋂ ∃hasColor."P" ⋂ ∃hasBook.RomanceBook ⋂ ∀inSection.RomanticSpiritualSection ...)
    - RedBookCase: contains adrenaline filled (action) books and has red colors, and it is placed in the Terrifying section
          (RedBookCase = BookCase ⋂ ∃hasColor."R" ⋂ ∃hasBook.SpiritualBook ⋂ ∀inSection.TerrifyingSection ...)
    - WhiteBookCase: contains eastern comic books and has white colors, and it is placed in the Art section
          (WhiteBookCase = BookCase ⋂ ∃hasColor."W" ⋂ ∃hasBook.EasternComicBook ⋂ ∀inSection.ArtSection ...)
    - YellowBookCase: contains meta physical books and has yellow colors, and it is placed in the philosophy section
          (YellowBookCase = BookCase ⋂ ∃hasColor."Y" ⋂ ∃hasBook.MetaPhysicalBook ⋂ ∀inSection.PhilosophySection)
   
All classes are disjoint except for the sub-classes of section, because some bookcases share the same room or some sensor are in the same room and this will cause inconsistency.

### Object Properties

1. hasBook: relation between a bookcase that has books in.
     (Domains = BookCase; Range = Book; Inverse of isBookOf)

2. hasBox: relation between a section or a bookcase that has a box.
     (Range = Box; Inverse of isBoxOf). The absence of domain is due to the fact that we want the union of Section class and BookCase one, but in protègè we can only have a intersection.

3. hasFinished: relation between a person that has finished some activities in the shop
     (Domain = Persona; Range = Engagement)

4. hasMobilePhone: relation between a person that has a mobile phone
     (Domain = Persona; Range = Sensor; Inverse of isMobilePhoneOf)

5. hasSensor: relation between a box or a section that has sensors inside/aside
     (Range = Sensor; Inverse of isSensorOf). Also here the domain is not considered.

6. hasBookCase: relation between a section where are placed bookcases
     (Domain = BookCase; Range = Section; Inverse of inSection)

7. inSection: Inverse of hasBookCase, so range and domain are inverted

8. isBookOf: Inverse of hasBook, so range and domain are inverted

9. isBoxOf: Inverse of hasBox, so range and domain are inverted

10. isLinked: relation between one section linked with another one
      (Domain = Section; Range= Section). It is avoided the reflective property because cause unexpected inconsistency in the ontology.

11. isMobilePhoneOf: Inverse of hasMobilePhone, so range and domain are inverted

12. isSensorOf: Inverse of hasSensor, so range and domain are inverted

13. overlap: relation between an Engagement class and a sensor
      (Domain = Engagement; Range = Sensor)

### Data Properties


1. hasBookNumber: number of books on a bookcase
     (Domain = BookCase; Range = xsd:integer)

2. hasPurchasedBook: number of books purchased by a person
     (Domain = Persona; Range = xsd:integer)

3. hasKey: barcode of 13 digits (randomly generated) on a book
     (Domain = RFIDAntennaSensor; Range = xsd:unsignedLong)

4. hasColor: color of a bookcase
     (Domain = BookCase; Range = xsd:string)

5. hasPriceCut: price cut of 20% if a person buy more than 2 books, data property created only for the SWRL rule
     (Domain = Persona; Range = xsd:decimal)

6. hasPage: number of pages of a book
     (Domain = Book; Range = xsd:int)

7. hasBookCaseNumber: number of bookcases in a section
     (Domain = Section; Range = xsd:int)

### ABox: Scenario

The ontology includes 111 individuals, reflecting a scenario where individuals Tayitu and Menelik enter the shop. Menelik makes several purchases, buying Naruto, One Piece, and The Big Book Of Faces.

#### SWRL Rule

Three SWRL rules have been implemented to enhance the functionality of the Ambient Book Shopping system:

1. **Price Cut Rule:**
   - **Objective:** Offer a 20% price cut on books if a person purchases more than two.
   - **SWRL Rule:**
     ```swrl
     Persona(?p) ^ hasPurchasedBook(?p, ?nb) ^ swrlb:greaterThan(?nb, 2) -> hasPriceCut(?p, 0.2)
     ```
   - **Explanation:** This rule dynamically applies a 20% price cut to the total purchase cost for individuals who buy more than two books, promoting bulk purchases.

2. **Access Section Engagement Rule:**
   - **Objective:** Capture an engagement when a person accesses a section.
   - **SWRL Rule:**
     ```swrl
     Persona(?p) ^ AccessedEngagement(?aeng) ^ hasMobilePhone(?p, ?phone) ^ isMobilePhoneOf(?phone, ?p) -> hasFinished(?p, ?aeng)
     ```
   - **Explanation:** This rule records the completion of an engagement when a person, identified as a persona, accesses a section in the bookshop. The presence of a mobile phone is a prerequisite.

3. **Purchase Book Engagement Rule:**
   - **Objective:** Capture an engagement when a person purchases a book.
   - **SWRL Rule:**
     ```swrl
     Persona(?p) ^ PurchaseBookEngagement(?peng) ^ hasMobilePhone(?p, ?phone) ^ isMobilePhoneOf(?phone, ?p) -> hasFinished(?p, ?peng)
     ```
   - **Explanation:** This rule registers the completion of an engagement when a person, represented as a persona, purchases a book. The rule requires a connection between the person and their mobile phone.

These rules collectively contribute to a seamless and intelligent book retail experience within the Ambient Book Shopping environment.



### Conclusion and Future Improvements

This ontology serves the assignment requirements, but for future applications in real-world smart environments, enhancements could include:

- Addition of an "Author" class for further book classification.
- Customization of the number of objects and sections based on seller preferences.

This project lays the foundation for a future where the love for reading thrives in technologically enriched spaces.
