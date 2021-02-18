### Τεχνολογία Λογισμικού - Εργαστήριο

__Zoom:__

    Meeting ID: 956 3491 4993
    Passcode: το όνομα του repo

Έναρξη εργαστηρίου:

    Πέμπτη, 18/2/2021, 09:00πμ

---

##### Περιβάλλον εργασίας

Για την υλοποίηση των εργασιών του εργαστηρίου θα πρέπει να εργαστείτε σε ένα Unix/Linux terminal. Θα αξιοποιήσετε κάποιες από τις ήδη διαθέσιμες εντολές του shell, αλλά θα χρειαστεί να εγκαταστήσετε και κάποια νέα προγράμματα.

Θα εργαστείτε καθένας στο δικό του περιβάλλον εκτέλεσης και θα πρέπει να εξοικειωθείτε με τον τρόπο που σας εξυπηρετεί καλύτερα. _Ενδεικτικά_ μπορείτε να επιλέξετε μπορείτε να αξιοποιήσετε μία από τις πιο κάτω _use yur own device_ επιλογές:
 * Αξιοποίηση ενός _reusable & disposable_ **linux docker container**, _οδηγίες πιο κάτω_
 * Ήδη εγκατεστημένο linux, πχ ως dual boot, όποια διανομή σας βολεύει/αρέσει
 * Εγκατάσταση ενός linux εντός virtual box
 * Αξιοποίηση Windows Linux Subsystem εφόσον το laptop σας τρέχει Win10, οδηγίες [εδώ](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
 * Χρήση _persistent live ubuntu usb_ (επιτρέπει την εκτέλεση XUbuntu Desktop περιβάλλοντος το οποίο διατηρεί τις αλλαγές που κάνετε, πχ εγκατάσταση προγραμμάτων)
   - Ακουλουθήστε [αυτές](https://www.howtogeek.com/howto/14912/create-a-persistent-bootable-ubuntu-usb-flash-drive/) τις οδηγίες και δημιουργήστε το δικό σας persistent live usb (αρκεί ένα usb flash drive 8GB, προτείνεται __USB3__)

   _linux = όποια διανομή σας βολεύει/αρέσει_

###### Οδηγίες αξιοποίησης docker container

Εγκαταστήστε στο συστημά σας το [docker](https://www.docker.com/).
* Ξεκινήστε ένα `container` βασισμένο πχ στο Ubuntu 20.04 `image`, μελετήστε [εδώ](https://www.docker.com/resources/what-container) τη διαφορά/σχέση images-containers:  
`docker run --name ionio-sw-lab -d -it ubuntu:20.04 `
    * Η παράμετρος `--name` ονοματίζει τον container ώστε να μπορούμε να το σταματήσουμε/ξεκινήσουμε εύκολα διατηρώντας της αλλαγές που κάνουμε
    * Η παράμετρος `--it` εξασφαλίζει ότι ο container, αφού δεν το ζητάμε να εκτελέσει κάποια εντολή ή πρόγραμμα, δεν θα τερματιστεί με την ολοκλήρωση της εντολής
    * Η διανομή που ξεκινάμε είναι `ubuntu` έκδοση `20.04`
    * _Tip_ Εκτελέστε την εντολή `docker ps` για να επιβεβαιώσετε ότι ο container σας τρέχει, να δείτε το container id του και το όνομά του:
    ```
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
    16a2dc0d7c03        ubuntu:20.04        "/bin/bash"         About an hour ago   Up About an hour                        ionio-sw-lab
    ```

* Συνδεθείτε στον container σας για να ξεκινήσουμε να δουλεύουμε εντός αυτού.  
`docker attach ionio-sw-lab`  
θα πρέπει να βρεθείτε εντός του container, σε ένα terminal και να μπορείτε να εκτελέσετε τυπικές εντολές bash:
```
root@16a2dc0d7c03:/# pwd
/
root@16a2dc0d7c03:/# whoami
root
```

* Ας δοκιμάσουμε να φτιάξουμε ένα φάκελο και ένα
αρχείο:  
```
root@16a2dc0d7c03:/# mkdir workspace
root@16a2dc0d7c03:/# touch workspace/hello    
root@16a2dc0d7c03:/# ls workspace/
hello
```

* Βγαίνουμε από τον container (και τον τερματίζουμε) με exit (ή Ctrl+D)
    * Αν τώρα εκτελέσετε `docker ps` **δεν** θα βλέπετε τον container σας, γιατί έχει σταματήσει. Εκτελέστε `docker ps -a` για να δείτε και τους σταματημένους containers:  
    ```
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
    16a2dc0d7c03        ubuntu:20.04        "/bin/bash"         About an hour ago   Exited (0) 2 minutes ago                       ionio-sw-lab
    ```

* Ξεκινάμε, πάλι:  
```docker start ionio-sw-lab```  
και συνδεόμαστε στον container:  
```docker attach ionio-sw-lab```  
ελέγχουμε αν οι αλλαγές μας έχουν διατηρηθεί:
```
root@16a2dc0d7c03:/# ls workspace/
hello
```

:fireworks: Έχουμε ένα persistent, reusable περιβάλλον (το οποίο εύκολα μπορούμε να ξαναδημιουργήσουμε εάν κάτι πάει στραβά!)

**ToDo (σας, <ins>για αυτή την εβδομάδα</ins>):**
1. Τροποποιήστε το prompt ώστε να δείχνει το ΑΜ σας _(hint: `PS1`;  αρχείο `/root/.bashrc`)_, πχ αλλαγή:  
```root@16a2dc0d7c03:```  
σε  
```Dr.DR  is root@16a2dc0d7c03:```  
    * Ελέγξτε εάν είναι persistent οι αλλαγές σας ;-)
2. Αν δεν έχετε ήδη (_πχ στο hci?_) δημιουργήστε (free) account στο [asciinema](https://asciinema.org/).
Χωρίς account οι καταγραφές που θα κάνετε κάνουν expire (σε ~15 ημέρες), άρα όταν έρθει η ώρα να αξιολογηθούν οι ασκήσεις σας.. _θα έχουν χαθεί_.  
Εγκαταστήστε το asciinema στο terminal περιβάλλον σας: `apt-get install asciinema` __και__ συνδέστε το terminal σας με το asciinema account σας με την εντολή `asciinema auth`.
    * Ελέγξτε το! Κάντε μια καταγραφή, ανεβάστε το στο asciinema, δοκιμάστε το url.
    * Μελετήστε τις οδηγίες του μαθήματος για τις προδιαγραφές των καταγραφών σας, πχ idle time!
3. Δημιουργία account στο github, με το ionio.gr e-mail σας.  
Fork το αποθετήριο του μαθηματος https://github.com/courses-ionio/sw.  
Κατέβασμα στο linux περιβάλλον σας. (Οδηγίες σύνδεσης linux+git+github [εδώ](https://kbroman.org/github_tutorial/pages/first_time.html) ή ακολουθήστε τα βασικά βήματα:)
    * Εγκαταστήστε το git στο περιβάλλον σας `apt-get install git`
    * Ρυθμίστε username και e-mail `git config --global user.name "Your name here"` και `git config --global user.email "...your_email...@ionio.gr"`
    * Προαιρετικά `git config --global color.ui true`
    * Δημιουργήστε ssh keys για διασύνδεση του περιβάλλοντος εργασίας σας με το github account σας.
        * Εκτελέστε `sh-keygen -t rsa -C "...your_email...@ionio.gr"` (δώστε ένα password που δεν θα ξεχάσετε, αφήστε το προτεινόμενο folder/file)
        * Αντιγράψτε το __δημόσιο__ κλειδί σας `cat ~/.ssh/id_rsa.pub` και μεταβείτε στο github:
            * Στο https://github.com/settings/keys σας και προσθέστε ένα νέο ssh key σας.
        * Ελέγξτε τη σύνδεση terminal-github με την εντολή  
        `ssh -T git@github.com`
            * Θα σας ζητήσει να αποδεχτείτε το fingerptint του πιστοποιητικού του github, αν σε ό,τι prompt βλέπετε σε ένα υπολογιστή πατάτε yes, τότε απλά πατήστε yes, διαφορετικά ελέγξτε το fingerprint [εδώ](https://docs.github.com/en/github/authenticating-to-github/githubs-ssh-key-fingerprints).
            * Θα σας ζητήσει το password που δώσατε τέσσερα bullets πριν, δεν το ξεχάσατε (ήδη.. ελπίζω :-)
            * Περιμένετε/ελπίζετε να δείτε κάτι σαν
            ```
            Hi riggas-ionio! You've successfully authenticated, but GitHub does not provide shell access.
            ```
    * Clone το __forked__ repository στο linux συστημά σας
        * Δημιουργήστε ένα local folder για να κατέβει το repo  
        `mkdir /workspace/github`  
        και μετάβαση εκεί  
        `cd /workspace/github`  
        * Εκτέλεση `git clone git@github.com:_____repo____.git`
        * _... κάνετε edit/add/commit (ό,τι ζητά η πρώτη εβδομάδα) ..._
        * Ανέβασμα από το περιβάλλον εργασίας στο github `git push origin master`
