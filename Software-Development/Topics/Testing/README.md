# Testing στην ανάπτυξη λογισμικού

- [Testing στην ανάπτυξη λογισμικού](#Testing-στην-ανάπτυξη-λογισμικού)
  - [Μαθησιακά αποτελέσματα:](#Μαθησιακά-αποτελέσματα)
  - [Importance of Testing:](#importance-of-testing)
  - [Σημασία του Testing:](#Σημασία-του-Testing)
  - [Είδη Testing:](#Είδη-Testing)
  - [Testing Προσεγγίσεων:](#Testing-Προσεγγίσεων)
  - [Testing Μέθοδοι:](#Testing-Μέθοδοι)
  - [Software Development Life Cycle (SDLC) and Testing:](#software-development-life-cycle-sdlc-and-testing)
  - [Popular Testing Tools:](#popular-testing-tools)
  - [Excercises and Assignments](#excercises-and-assignments)

## Μαθησιακά αποτελέσματα:

Αφού ολοκληρώσετε αυτό τη θεματική ενότητα, θα είστε σε θέση να:

- κατανοήσετε τη σημασία του testing στην ανάπτυξη λογισμικού,
- προσδιορίσετε τους διάφορους τύπους testing,
- περιγράψετε διάφορες προσεγγίσεις και μεθόδους testing,
- να εφαρμόζουν τις αρχές του testing στην ανάπτυξη λογισμικού.

Το testing στην ανάπτυξη λογισμικού αναφέρεται στη διαδικασία εκτέλεσης ενός προγράμματος ή μιας εφαρμογής με σκοπό την εύρεση σφαλμάτων λογισμικού. Διασφαλίζει ότι το προϊόν λογισμικού πληροί τις καθορισμένες απαιτήσεις και παραδίδει ένα ποιοτικό προϊόν στον τελικό χρήστη.


## Σημασία του Testing:

- **Διασφάλιση ποιότητας:** Διασφαλίζει ότι το προϊόν πληροί τα επιθυμητά πρότυπα ποιότητας και είναι απαλλαγμένο από ελαττώματα.
- **Αποδοτικό από πλευράς κόστους:** Ο εντοπισμός και η επιδιόρθωση προβλημάτων σε πρώιμο στάδιο του κύκλου ζωής της ανάπτυξης μπορεί να εξοικονομήσει χρήματα μακροπρόθεσμα.
- **Ασφάλεια:** Βοηθά στον εντοπισμό τρωτών σημείων και αδυναμιών στο λογισμικό.
- **Ικανοποίηση χρηστών:** Διασφαλίζει ότι το προϊόν ευθυγραμμίζεται με τις απαιτήσεις των χρηστών και μπορεί να χρησιμοποιηθεί αποτελεσματικά.
- **Αξιοπιστία και απόδοση:** Διασφαλίζει τη βέλτιστη απόδοση του λογισμικού υπό πίεση και την αξιοπιστία του σε διάφορες συνθήκες.

## Είδη Testing:

- **Unit Testing:** Δοκιμές μεμονωμένων μονάδων ή στοιχείων του λογισμικού.

- **Testing Eνσωμάτωσης:** Δοκιμή αλληλεπιδράσεων μεταξύ ολοκληρωμένων μονάδων για την παραγωγή εκροών.

- **Functional Testing:** Testing του λογισμικού για να διασφαλιστεί ότι συμπεριφέρεται σύμφωνα με τις καθορισμένες απαιτήσεις.
  
- **System Testing:** Testing του λογισμικού ως πλήρες σύστημα για να διασφαλιστεί ότι λειτουργεί όπως αναμένεται.

- **End-to-End Testing:** Testing της ροής μιας εφαρμογής για να διασφαλιστεί η ομαλή λειτουργία ολόκληρης της διαδικασίας εισόδου και εξόδου του χρήστη.

- **Testing παλινδρόμησης:** Διασφάλιση ότι οι νέες αλλαγές στον κώδικα δεν έχουν επηρεάσει αρνητικά τις υπάρχουσες λειτουργίες.

- **Acceptance Testing:** Διασφάλιση ότι το λογισμικό πληροί τα κριτήρια αποδοχής πριν από την παράδοση στον πελάτη.

- **Performance Testing:** Αξιολόγηση των επιδόσεων, της ταχύτητας και της απόκρισης του λογισμικού. Οι υποκατηγορίες περιλαμβάνουν Load Testing, Stress Testing, και Volume Testing.

- **Usability Testing:** Αξιολόγηση του λογισμικού από τη σκοπιά του τελικού χρήστη για να διασφαλιστεί ότι είναι φιλικό προς το χρήστη.

- **Security Testing:** Εντοπισμός τρωτών σημείων, απειλών, κινδύνων σε μια εφαρμογή λογισμικού.

- **Compatibility Testing:** Διασφάλιση της συμβατότητας του λογισμικού σε διαφορετικές συσκευές, προγράμματα περιήγησης και λειτουργικά συστήματα.

- **Exploratory Testing:** Μη δομημένη προσέγγιση όπου οι ελεγκτές εξερευνούν ενεργά την εφαρμογή για να βρουν ελαττώματα.

## Testing Προσεγγίσεων :

- **Manual Testing:** Οι δοκιμαστές εκτελούν τις περιπτώσεις δοκιμών χειροκίνητα χωρίς καμία υποστήριξη από εργαλεία. Πρόκειται για πρακτική εργασία και ο ελεγκτής πρέπει να είναι οξυδερκής παρατηρητής. 

- **Automated Testing:** Οι περιπτώσεις δοκιμών εκτελούνται με τη βοήθεια εργαλείων, σεναρίων και λογισμικού. Αυτή η προσέγγιση είναι επωφελής για δοκιμές παλινδρόμησης, δοκιμές φορτίου και επαναλαμβανόμενες εργασίες.

## Testing Μέθοδοι:

- **White Box Testing (or Glass Box Testing):** Δοκιμές με βάση τον εσωτερικό κώδικα, το σχεδιασμό και τη δομή του λογισμικού. Απαιτεί γνώση του κώδικα.

- **Black Box Testing:** Δοκιμές με βάση τις απαιτήσεις και τη λειτουργικότητα του λογισμικού, χωρίς γνώση των εσωτερικών λειτουργιών.

- **Grey Box Testing:** Ένας συνδυασμός White και Black Box Testing.

## Software Development Life Cycle (SDLC) and Testing:

- **Waterfall Model:** Το Testing ξεκινά μόνο μετά την ολοκλήρωση της ανάπτυξης.

- **Agile Model:** Testing is concurrent with development and is iterative.

- **V-Model (Validation and Verification):** Development and testing happen concurrently, with each development stage having a corresponding testing phase.

## Popular Testing Tools:

- **JUnit:** A widely-used testing tool for Java.

- **Selenium:** A powerful tool for controlling a web browser through programs.

- **QTP (Quick Test Professional):** An automated functional testing tool.

- **LoadRunner:** A performance testing tool.

- **TestNG:** Inspired by JUnit and designed for test configuration and parallel execution.

- **NUnit:** A unit-testing framework for .NET languages.

In conclusion, testing is an integral part of software development that ensures the delivery of a robust, high-quality product. It identifies and rectifies bugs, vulnerabilities, and deficiencies in the early stages, ensuring the software meets user expectations and industry standards. Proper testing results in reliable software, minimizes risks, and enhances user satisfaction.

## Excercises and Assignments

