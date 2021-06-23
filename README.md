# PARALLEL

Η ολική βελτιστοποίηση αποτελεί ένα από τα σημαντικότερα θέματα έρευνας στον τομέα των εφαρμοσμένων μαθηματικών. Έχει πολύ σημαντικές εφαρμογές σε διάφορα πεδία επιστημών, όπως οικονομία, χημεία, βιολογία και μηχανική.
Στόχος της ολικής βελτιστοποίησης είναι η εύρεση μίας λύσης εντός ενός συνόλου λύσεων στο οποίο η αντικειμενική συνάρτηση αποκτά τη μικρότερη τιμή της, δηλαδή το ολικό ελάχιστο. Επομένως, η ολική βελτιστοποίηση δεν στοχεύει απλά στον καθορισμό ενός τοπικού ελαχίστου αλλά στο μικρότερο τοπικό ελάχιστο από το σύνολο των λύσεων.
Για την εύρεση ενός τοπικού ελαχίστου έχουν προταθεί διάφορες μέθοδοι. Η μέθοδος άμεσης αναζήτησης των Hooke και Jeeves εκτελεί ευθύγραμμη αναζήτηση από το τρέχον σημείο προς συγκεκριμένες διευθύνσεις. Εφόσον βρεθεί κάποιο νέο σημείο με καλύτερη συναρτησιακή τιμή τότε η μέθοδος αντικαθιστά το τρέχον σημείο με το νέο. Διαφορετικά, προσαρμόζει τις παραμέτρους της ευθύγραμμης αναζήτησης και επαναλαμβάνει τη διαδικασία στο ίδιο σημείο.
Μια υλοποίηση της μεθόδου Hooke-Jeeves υπάρχει στη NetLib, και συγκεκριμένο στο αρχείο http://www.netlib.org/opt/hooke.c. Η συνάρτηση υπολογίζει ένα σημείο Χ στο οποίο η μη γραμμική συνάρτηση f(X) έχει ένα τοπικό ελάχιστο. Το σημείο Χ είναι ένα Ν-διάστατο διάνυσμα και η τιμή της συνάρτησης f(X) είναι βαθμωτή (scalar), δηλαδή ισχύει ότι f: Rn → R1.
Η αντικειμενική συνάρτηση που θα χρησιμοποιηθεί στα πλαίσια της εργασίας του μαθήματος είναι η συνάρτηση Rosenbrock, η οποία ορίζεται ως εξής:
Η συνάρτηση έχει καθολικό ελάχιστο στο σημείο (1,1,...,1), όπου παίρνει την τιμή 0. Για περισσότερες πληροφορίες: http://en.wikipedia.org/wiki/Rosenbrock_function.
Μια προφανής πιθανοτική διαδικασία ολικής βελτιστοποίησης βασίζεται στην εφαρμογή ενός αλγορίθμου τοπικής βελτιστοποίησης σε διαφορετικά σημεία της συνολικής περιοχής αναζήτησης. Η διαδικασία καλείται "Multistart" (Πολυεναρκτήρια Τοπική Αναζήτηση), με τα σημεία στα οποία εφαρμόζεται η τοπική βελτιστοποίηση να επιλέγονται με τυχαίο τρόπο.
2. Λογισμικό Ολικής Βελτιστοποίησης
H παρούσα εργασία περιλαμβάνει μία εφαρμογή (multistart_hook_seq.c) pπου υλοποιεί σειριακά τη μέθοδο Multistart σύμφωνα με την περιγραφή στην προηγούμενη ενότητα. Η εφαρμογή επιλέγει ntrials τυχαία σημεία διάστασης nvars, καλεί τη μέθοδο Hooke-Jeeves σε καθένα από αυτά για να βρει το τοπικό ελάχιστο και υπολογίζει το σημείο εκείνο που δίνει το ολικό ελάχιστο για τη συνάρτηση Rosenbrock, εκτυπώνοντας τελικά το σημείο αυτό καθώς και την τιμή της συνάρτησης στο συγκεκριμένο σημείο. Ως πεδίο αναζήτησης χρησιμοποιείται το διάστημα [-4, 4) για κάθε μια από τις nvars διαστάσεις της
   1
Τμήμα Μηχ. Η/Υ και Πληροφορικής, Πανεπιστήμιο Πατρών
συνάρτησης. Επίσης χρησιμοποιούνται οι εξ' ορισμού τιμές για τις παραμέτρους της μεθόδου, όπως αυτές ορίζονται στο αρχείο από τη NetLib.
3. Παράλληλη Ολική Βελτιστοποίηση
Βασικός στόχος της εργασίας είναι η παραλληλοποίηση του λογισμικού ολικής βελτιστοποίησης, χρησιμοποιώντας τα διάφορα μοντέλο προγραμματισμού που μελετήθηκαν στα πλαίσια του μαθήματος. Συγκεκριμένα, η μέθοδος Hooke-Jeeves θα πρέπει να εφαρμοστεί παράλληλα στα τυχαία σημεία που επιλέγονται από την εφαρμογή. Βασικός στόχος της παράλληλης υλοποίησης είναι η ελαχιστοποίηση του χρόνου εύρεσης των τοπικών ελαχίστων που υπολογίζονται από τη συνάρτηση Hooke-Jeeves και η τελική εύρεση του σημείου που αντιστοιχεί στο ολικό ελάχιστο.
Τα μοντέλα προγραμματισμού τα οποία θα χρησιμοποιήσετε για την παραλληλοποίηση της εφαρμογής είναι τα ακόλουθα:
• OpenMP: πολλαπλά νήματα εφαρμόζουν τη μέθοδο στα τυχαία σημεία.
• OpenMP tasks: όπως πριν αλλά χρησιμοποιώντας τo μοντέλο εργασιών του OpenMP.
• MPI: πολλαπλές διεργασίες εφαρμόζουν τη μέθοδο στα τυχαία σημεία.
• MPI+OpenMP: υβριδικό μοντέλο προγραμματισμού, με πολλαπλά νήματα ανά MPI διεργασία.
4. Μετρήσεις
Αφού ολοκληρώσετε τις παράλληλες εκδόσεις της εφαρμογής και βεβαιωθείτε για τη σωστή λειτουργίας τους, θα μετρήσετε την απόδοσή τους ώστε να δείξετε την σωστή αξιοποίηση του διαθέσιμου πολυεπεξεργαστικού υλικού. Για κάθε μοντέλο προγραμματισμού θα πρέπει να μετρήσετε το χρόνο εκτέλεσης της εφαρμογής, δηλ. το χρόνο υπολογισμού των τοπικών ελαχίστων, για διάφορους αριθμούς επεξεργαστικών στοιχείων (νημάτων / διεργασιών κλπ). Για κάθε μοντέλο, μας ενδιαφέρει τόσο ο ελάχιστος χρόνος εκτέλεσης όσο και η χρονοβελτίωση (speedup) της εφαρμογής.
Ως σημείο αναφοράς για τα πειράματά σας, αρχικοποιήστε τη γεννήτρια τυχαίων αριθμών με φύτρο (seed) ίσο με ένα (π.χ. srand48(1)) και υπολογίστε τα τοπικά ελάχιστα της συνάρτησης Rosenbrock για 128Κ σημεία διάστασης 16.
