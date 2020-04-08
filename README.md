# Εργαστήριο μαθήματος Τεχνολογία Λογισμικού
---
Για την υλοποίηση των εργασιών του εργαστηρίου θα πρέπει να εργαστείτε σε ένα Unix/Linux terminal. Θα αξιοποιήσετε κάποιες από τις ήδη διαθέσιμες εντολές του shell, αλλά θα χρειαστεί να εγκαταστήσετε και κάποια νέα προγράμματα.

Για να εργαστείτε καθένας στο δικό του περιβάλλον εκτέλεσης, μπορείτε να αξιοποιήσετε όποια από τις πιο κάτω επιλογές σας εξυπηρετεί καλύτερα:
 * _Bring your own laptop:_ Ιδανικά με ήδη εγκατεστημένο linux, πχ ως dual boot
 * _Bring your own laptop:_ Εγκατάσταση ενός linux εντός virtual box
 * _Bring your own laptop:_ Αξιοποίηση Windows Linux Subsystem εφόσον το laptop σας τρέχει Win10
 * Χρήση _persistent live ubuntu usb_ (επιτρέπει την εκτέλεση XUbuntu Desktop περιβάλλοντος το οποίο διατηρεί τις αλλαγές που κάνετε, πχ εγκατάσταση προγραμμάτων)
   - Ακουλουθήστε [αυτές](https://www.howtogeek.com/howto/14912/create-a-persistent-bootable-ubuntu-usb-flash-drive/) τις οδηγίες και δημιουργήστε το δικό σας persistent live usb

---
### Υλικό εργαστηρίου

1. Εργαστήριο #1 - Εισαγωγή στο Unix/Linux shell
   * [Learning the bash Shell, 3rd Edition](https://www.google.com/search?q=Learning+the+bash+Shell%2C+3rd+Edition)
2. Εργαστήριο #2 - Εγκατάσταση προγραμμάτων μέσω του terminal
   * Εγκαταστήστε το [homebrew](https://docs.brew.sh/Homebrew-on-Linux) στο Linux σύστημά σας, παρότι ___υπάρχουν κάποια security concerns___, πχ [εδώ](https://discourse.brew.sh/t/security-issues-using-homebrew-malicious-insertion/3379/2), η χρήση του σε ένα περιορισμένο, εκπαιδευτικό περιβάλλον θα διευκολύνει πολύ την εγκατάσταση των απαιτούμενων προγραμμάτων
     - Η εγκατάσταση του Homebrew προαπαιτεί τη παρουσία διαφόρων λογισμικών, όπως πχ git, τα οποία μπορεί να λείπουν από το περιβάλλον σας και τα οποία θα πρέπει να εγκαταστήσετε - σε περιβάλλον ubuntu αυτό μπορείτε να το πετύχετε ως superuser με την εντολή `sudo apt-get install <package-name>`
   * Εγκατάσταση [asciinema](https://asciinema.org/docs/installation), πχ μέσω brew
     - Ν.Β.: κάνετε sign up στο asciinema, διαφορετικά οι _καταγραφές_ σας σβύνονται μετά από μερικές μέρες, άρα _όταν πρόκειται να διορθωνούν δε θα υπάρχουν!_
   * Εγκατάσταση των
     - [cheat](https://github.com/cheat/cheat)
     - [tldr](https://tldr.sh/)
     - [neofetch](https://github.com/dylanaraps/neofetch)
   * Εξάσκηση στη χρήση του asciinema
     - Έναρξη καταγραφής `asciinema rec`
     - _εκτέλεση shell εντολών της επιλογής σας, πχ χρήση `nano`, `source`, `PS1` για αλλαγή του command prompt του terminal_
     - Παύση καταγραφής `exit`
     - Για τοπική αποθήκευση `Ctrl+C`
       - σημειώστε το `/path/to/file.cast`
     - Αναπαραγωγή καταγραφής `asciinema play /path/to/file.cast`
   * Μελετήστε τις παραμέτρους που μπορεί να πάρει η `asciinema` και
     - ελαχιστοποιήστε το idle recording time σε <0.5 sec
     - προσθέστε ένα τίτλο στην καταγραφή
3. Εργαστήριο #3 - Benchmarking python code
   * Εγκαταστήστε benchmarking και performance monitoring εργαλεία, όπως τα προτεινόμενα `hyperfine` και `py-spy` και εκτελέστε I/O ή CPU intensive κώδικα python ώστε να αξιολογήσετε την απόδοσή του ή σημεία που με τη βελτίωσή τους η συνολική απόδοση θα μπορούσε να αυξηθεί.
   * Μπορείτε να κάνετε την εγκατάσταση των
     - [hyperfine](https://github.com/sharkdp/hyperfine) μέσω `brew`
     - [py-spy](https://github.com/benfred/py-spy) μέσω `pip3` (ίσως πρέπει να εγκατασταθεί στο σύστημά σας). _Ειδικά για το py-spy λάβετε υπόψη σας [αυτό](https://github.com/benfred/py-spy/blob/master/README.md#when-do-you-need-to-run-as-sudo) και ίσως χρειαστει να εγκαταστείσετε το py-spy και ως su_
   * Εξάσκηση στη χρήση του py-spy & του hiperfine
     - Χρησιμοποιήστε τον κώδικα στο [lab3/rand_ints.py](./lab3/rand_ints.py) για να παράγετε αρχεία τυχαίων ακεραίων αριθμων.
     - Χρησιμοποιήστε τον κώδικα στο [lab3/bubble.py](./lab3/bubble.py) για να ταξιμονήσετε τα αρχεία τυχαίων ακεραίων αριθμων που παράγατε.
     - Χρησιμοποιήστε το hyperfine για να δείτε το χρόνο εκτέλεσης της bubble sort ταξινόμησης
       - Πειραματιστείτε με παραμέτρους που μπορείτε να δώσετε στο hyperfine, πχ `--warmup`
     - Αξιολογήστε την απόδση του bubble sort σε σχέση με άλλους sorting αλγορίθμους, πχ insertionsort ή quicksort, τους οποίους βρείτε ή υλοποιήστε [;-)](https://medium.com/@george.seif94/a-tour-of-the-top-5-sorting-algorithms-with-python-code-43ea9aa02889)
     - Χρησιμοποιήστε το py-spy για να δείτε ποιο τμήμα ενός αλγορίθμου ταξινόμησης αναλώνει το μεγαλύτερο χρονικό διάστημα κατά την εκτέλεσή του
       - Ερμηνεύστε το svg που παράγει, πώς μπορείτε να το αξιοποίησετε για το profiling/benchmarking ενός κώδικα;
4. Εργαστήριο #4 - Using the terminal as an ide
    * Εγκαταστήστε μερικά plugin στο vi, π.χ.:
      - `vim-plug` minimalist Vim plugin manager
      - `python-mode` a Python IDE for Vim
    * Εγκαταστήστε μερικά python development εργαλεία, π.χ.:
     - `pylint` a tool that checks for errors in Python code, tries to enforce a coding standard and looks for code smells
    * Εξάσκηση στη χρήση vim ως python IDE:
      - Αναπτύξτε ένα σύντομο κώδικα σε python αξιοποιώντας το vim ως IDE. Κάντε debug και εκτελέστε τον κώδικά σας απ' ευθείας μέσα από το vim με εντολές του python-mode.
      - Βρείτε και εγκαταστήστε ένα git plugin και δείξτε την αξιοποίηση του git μέσα από το vim.
      - Εγκαταστήστε ένα plugin για άλλη γλώσσα προγραμματισμού της επιλογής σας, ώστε να αξιοποιήσετε το vim ως IDE και γι αυτή.
5. Εργαστήριο #5 - Αξιοποιήστε το σύστημά σας για ανάπτυξη ανεξάρτητων python projects
   * Εγκαταστήστε τα `pip3`, `pipenv` και `virtualenv`, δείτε εδώ:
   https://asciinema.org/a/bmEf1BiVyWvmbld5SyQK0ORYW
   * Δημιουργήστε ένα environment εγκαταστήστε εντός αυτού ένα module, πχ `psutil` και γράψτε κώδικα που το χρησιμοποιεί. Εαν αντιγράψετε αυτό τον κώδικα σε άλλο φάκελο, ο κώδικας έχει ένα unsatified dependency!.. Τέλεια, πετύχατε isolation των project σας.
   https://asciinema.org/a/6450xvAveLYOQXcMfrdN7oKM2
   * Και αν θέλετε να _μεταφέρετε_ τα requirements από ένα project σε ένα άλλο;
   https://asciinema.org/a/kzrRIfVi4u2tH4gSlpG9oapiJ
6. Εργαστήριο #6 - Εκτελέστε _βαριές_ εργασίες στο background του terminal σας και λάβετε ειδοποίηση όταν αυτή έχει ολοκληρωθεί
   * Εγκαταστήστε το `ntfy` και κάνετε το απαραίτητο configuration για να στέλνει τις ειδοποιήσεις του στο syslog του συστήματός σας.
     - Βεβαιωθείτε ότι το `/var/log/syslog` υπάρχει και ενημερώνεται. Αν όχι, βεβαιωθείτε για την εγκατάσταση του σχετικου deamon με την εντολή `sudo apt-get install --reinstall rsyslog` και στη συνέχεια βεβαιωθείτε για την ενεργοποίησή του με την εντολή `sudo service rsyslog restart`.
     - Ελέγξτε ότι το syslog γράφεται, εκτελέστε την εντολή `logger Hello logger service!` (δεν χρεάζεται quotes) και ελέγξτε ότι γράφτηκε το μήνυμα στο αρχείο syslog με την εντολή `tail /var/log/syslog`.
   * Κάνετε configure το ntfy (δημιουργήστε ή ενημερώστε το `ntfy.yml` αρχείο σας) ώστε να στέλνει τις ειδοποιήσεις του στο syslog.
   * Βεβαιωθείτε ότι υπάρχει εγκατεστημένο το python module `psutil` εγκατεστημένο στο σύστημά σας (_αν όχι_, `pip install psutil` ;-)
   * **Checkpoint**: η εκτέλεση `ntfy done -h` στο terminal σας εμφανίζει (μεταξύ άλλων) _-p PID, --pid PID     Watch a PID instead of running a new command_
   * Εκτελέστε κάποιο κώδικα ο οποίος χρειάζεται χρόνο για την εκτέλεσή του. Παράδειγμα θα ήταν ένας κώδικας σε python ο οποίος υπολογίζει τον ν-οστό _πρώτο_ αριθμό.
   * Ξεκινήστε την εκτέλεση του _αργού κώδικα_ στέλνοντας την εκτέλεση στο background του terminal (με χρήση `&`), πάρτε το pid και δώστε το στο ntfy ώστε να σας ενημερώσει όταν ολοκληρωθεί αυτό το process, πάλι στο background. Κάντε `tail -f` στο syslog και περιμένετε την ενημέρωση από το ntfy.
