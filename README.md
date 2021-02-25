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
        * Εκτελέστε `ssh-keygen -t rsa -C "...your_email...@ionio.gr"` (δώστε ένα password που δεν θα ξεχάσετε, αφήστε το προτεινόμενο folder/file)
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

---

##### CV

Για την εργασία cv θα πρέπει να αξιοποιήσουμε αρχικά το Jekyll (static site generator) και στη συνέχεια pandoc.  
Φυσικά (!) θα δουλέψουμε μέσα στο docker container που έχουμε ήδη φτιάξει.. οπότε κάντε τα δέοντα docker start και attach.  
Εντός του container πλέον:  
* Εγκατάσταση ruby, jekyll, κλπ προαπαιτούμενα, αναλυτικά [εδώ](https://jekyllrb.com/docs/installation/) <sub>...245+ΜΒ, θέλει χρόνο... :-( </sub>
    ```
    apt-get install ruby-full build-essential zlib1g-dev
    echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
    echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
    echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
    source ~/.bashrc
    gem install jekyll bundler
    ```
    * Test flight του jekyll, ας κάνουμε ένα δοκιμαστικό static web
    :-)
        * Ας φτιάξουμε ένα folder για το project μας  
        `mkdir /workspace/jekyll` και ας μεταβούμε σε αυτό  
        `cd /workspace/jekyll`
        * Αξιοποιούμε το bundler που εγκαταστήσαμε νωρίτερα `bundle init`
        * Προσθέτουμε το `gem "jekyll"` ως dependency στην τελευταία γραμμή του Gemfile που μόλις δημιουργήθηκε.  
        __Προσοχή:__ να μην ξεκινά και αυτή η γραμμή με # όπως η `# gem "rails"` γιατί τότε θα είναι σχόλιο!!
        * Εκτελούμε `bundler` και το project μας αποκτά όλα τα ruby gems που απαιτούνται
        * Ας δημιουργήσουμε το περιεχόμενό μας:
            * Πρώτα ένα folder για το περιεχόμενό μας `mkdir /workspace/jekyll/site`
            * Μετά το index.html αρχείο `vi site/index.html` με (ενδεικτικό) περιεχόμενο:  
            ```
            <!DOCTYPE html>
            <html>
              <head>
                <meta charset="utf-8">
                <title>Dr's Home</title>
              </head>
              <body>
                <h1>Hello World, this is the Dr!</h1>
              </body>
            </html>
            ```
        * Μέχρι εδώ δημιουργήσαμε την πρώτη ύλη του site μας, τώρα ας ζητήσουμε από το jekyll να δημιουργήσει το site μας.. (οκ, σε αυτό το site που δεν έχουν χρησιμιποιήσει templates, variables κλπ δεν θα  αλλάξει κάτι) `bundle exec jekyll build` και βλέπουμε κάτι σαν:  
        ```
        Configuration file: none
                Source: /workspace/jekyll
                Destination: /workspace/jekyll/_site
                Incremental build: disabled. Enable with --incremental
                Generating...
                    done in 0.01 seconds.
                Auto-regeneration: disabled. Use --watch to enable.
        ```
        * Ας δούμε το site μας... `jekyll serve --host 0.0.0.0 &`. Το site είναι διαθέσιμο στο `http://localhost:4000` (και σε κάθε άλλη ip που ακούει ο container αφού χρησιμοποιήσαμε το `--host 0.0.0.0`). Πώς θα το δούμε;
            * Από το terminal πχ με lynx. Εγκαθιστούμε `apt-get install lynx` - χρησιμοποιούμε `lynx localhost:4000/site`
            * Από το pc μας?
                * Το localhost του docker container __δεν__ είναι το localhost του μηχανήματός μας! Αλλά μπορούμε να κάνουμε port mapping από ένα port του μηχανήματός μας σε ένα port εντός του docker. Αυτό, βέβαια, κανονικά γίνεται κατά τη δημιουργία του container.. αλλά θα τα καταφέρουμε..  
                Πώς;
                    * Βγαίνουμε από τον container μας και τον τερματίζουμε:  
                    `docker stop __container_name__`
                    * Δημιουργούμε ένα image με βάση τον container μας:  
                    `docker commit __container_name__ __container_name__-img`
                    * Ξεκινάμε ένα __νέο__ container με βάση το image που μόλις δημιουργήσαμε __και__ port mapping από το 8080 του μηχανήματός μας στο 4000 εντός του νέου container:  
                    `docker run --name ionio-sw-lab2 -p 8080:4000 -it ionio-sw-lab-img`
                    * Πάμε στο folder `cd /workspace/jekyll/` και τρέχουμε πάλι το `jekyll serve --host 0.0.0.0 &`
                    * Πάμε σε ένα browser στο pc μας, δίνουμε διεύθυνση `http://0.0.0.0:8080/site/` και... βλέπουμε το site της μίας γραμμής που έχουμε φτιάξει ως εδώ.
        * Cleaning up.. έχουμε ένα άχρηστο πλέον container, το ionio-sw-lab της περασμένης εβδομάδας, αφού μόλις δημιουργήσαμε ένα κλώνο του με port mapping. Ας το ξεφορτωθούμε και ας αλλάξουμε όνομα στο νέο container μας.
            * Διαγραφή παλιού container `docker rm ionio-sw-lab`
            * Μετονομασία νέου `rename ionio-sw-lab2 ionio-sw-lab` (μπορεί να γίνει όσο τρέχει)

    * Τώρα ας ξεκινήσουμε να φτιάχνουμε ένα site που θα περιέχει το cv μας.
        * Νέο site.. = νέο folder για το project μας  
        `mkdir /workspace/cv` και ας μεταβούμε σε αυτό  
        `cd /workspace/cv`
        * Αρχικοποιούμε όπως πριν... _bundler κλπ_
        * Δημιουργούμε folder `mkdir /workspace/cv/site` και __διαχωρίζουμε μορφή από περιεχόμενο__:
            * Αρχείο view `vi /workspace/cv/site/index.html`, προσέξτε την αλλαγή με την προσθήκη δύο γραμμών `---` στην αρχή του αρχείου και `{{...}}` με ονόματα μεταβλητών:  
            ```
             ---
             ---
            <!DOCTYPE html>
            <html>
              <head>
                <meta charset="utf-8">
                <title>{{site.data.details.name}}'s Home</title>
              </head>
              <body>
                <h1>Hello World, this is the {{site.data.details.name}}!</h1>
              </body>
            </html>
            ```
            * Αρχείο data `vi /workspace/cv/_data/details.yml`, προσέξτε το αρχείο να ξεκινάει με μία γραμμή `---` και κάθε _μεταβλητή_ που θέλουμε να είναι διαθέσιμη στο παραγώμενο html να είναι _κλειδί_ στο yml αρχείο:
                * btw.. λίγα λόγια για το [YAML](https://www.cloudbees.com/blog/yaml-tutorial-everything-you-need-get-started/)

            ```
             ---
            # Personal details
            name: Friedrich Nietzsche
            urls:
             - wki.pe/friedrich_nietzsche
             - twitter.com/tinynietzsche
            ```
            * Τρέχουμε το `jekyll serve --host 0.0.0.0 &` (αν τρέχει κάποιο άλλο jekyll, κάντε το kill) ελέγχουμε και... βλέπουμε ένα site στο οποίο τα δεδομένα διαχωρίζονται από την εμφάνιση!
            * Αλλάζουμε το index.html αρχείο για να δείχνει και τα url με ένα for loop:
            ```
             ---
             ---
            <!DOCTYPE html>
            <html>
              <head>
                <meta charset="utf-8">
                <title>{{site.data.details.name}}'s Home</title>
              </head>
              <body>
                <h1>Hello World, this is the {{site.data.details.name}}!</h1>
                <p>Reach me at:
                <ul>
                  {% for url in site.data.details.urls %}
                    <li><a href="http://{{url}}">{{url}}</a></li>
                  {% endfor %}
                </ul>
              </body>
            </html>
            ```
            * :-) τέλεια!  

    * Τελειώσαμε;.. όχι, αρχίζουμε!   

        * Ας δημιουργήσουμε ένα νέο repository, έστω `cv-1`, public repository με ένα README.md.
        * Στο github κάνουμε τις ρυθμίσεις `Settings` > βασική σελίδα, πολύ χαμηλά `GitHub Pages`.
            * Source branch το __master__ και folder το __/__ (root)
            * Αφήνουμε να προσθέσει sample περιεχόμενο README.md αρχείο
                * Τώρα κάθε φορά που θα κάνουμε ένα commit, θα τρέχει το jekyll και ό,τι παράγεται θα πηγαίνει στο github pages ως rendered html site.
        * Αφήνουμε το github repo ως έχει και πάμε πίσω στο container μας.
            * Πάμε στο `cd /workspace/github` και yet another jekyll site: `mkdir cv`, `cd cv`.
        * Αξιοποιούμε το bundler που εγκαταστήσαμε νωρίτερα `bundle init`
        * Προσθέτουμε στο τέλος του Gemfile που μόλις δημιουργήθηκε:
            ```
            gem "jekyll", "~> 3.9.0"
            gem "github-pages","~> 212" , group: :jekyll_plugins
            group :jekyll_plugins do
              gem "jekyll-feed", "~> 0.15.1"
            end
            ```
            Προσοχή συμβουλευόμαστε το github gem dependencies [εδώ](https://pages.github.com/versions/)!
        * Εκτελούμε `bundler` και το project μας αποκτά όλα τα ruby gems που απαιτούνται
        * Κόβουμε δρόμο και φέρνουμε σε αυτό το project τα:
            * `cp -r /workspace/cv/_data/ .`
            * `cp /workspace/cv/site/index.html .`
        * _Για να μην αντιμετωπίσουμε πρόβλημα με την κωδικοποίηση χαρακτήρων.._
            * `apt-get install -y locales`
            * `echo "en_US UTF-8" > /etc/locale.gen`
            * `locale-gen en_US.UTF-8`
            * `export LANG=en_US.UTF-8`
            * `export LANGUAGE=en_US:en`
            * `export LC_ALL=en_US.UTF-8`
                * _τα τρία τελευταία προσθέστε τα στο τέλος του `/root/.bashrc`_
        * Σύνδεση με github repository  
            * `git init`
            * `git remote add origin git@github.com:riggas-ionio/cv-1.git`
            * `git add index.html`
            * `git add _data/`            
        * Είμαστε έτοιμοι για `bundle exec jekyll build`
        * Και.. `bundle exec jekyll serve --host 0.0.0.0 &`
            * Test σε browser..! ;-)
                * http://localhost:8080/ δείχνει σωστά
                * https://riggas-ionio.github.io/cv-1/ ... όχι... 8-(  
                γιατί το πρώτο το βλέπουμε από το jekyll εντός του container, δεν έχει ανέβει ακόμη στο github ώστε να γίνει build και να σταλεί στο github pages.  
                Άρα..
        * Commit και push..
            * `git commit -m "Ιnitial CV commit"`
            * `git push -u origin master`  
            Με το push στο __github.com__ το site γινεται _build_ και ανεβαίνει και στο __github.io__ (Github Pages)!

**ToDo (σας, <ins>για αυτή την εβδομάδα</ins>):**
1. Δείτε ένα πιο πλήρες yml για CV [εδώ](https://github.com/mrzool/cv-boilerplate)  
2. Συμπληρώστε τα στοιχεία σας (ή τέλος πάντων αρκετά) στο `_data/details.yml` και δημιουργήστε το κατάλληλο `index.html` για την προβολή τους.
    * Τσεκάρετε τακτικά locally, όταν είστε ικανοποιημένοι ανεβάστε στο github με push
3. Φροντίστε για έχετε καταγράψει στο asciinema τη δουλεία σας
4. Κάντε commit την πρόοδό σας
