### Τεχνολογία Λογισμικού - Εργαστήριο


Έναρξη εργαστηρίου:

    Πέμπτη, 17/2/2021, 11:00πμ - εργαστήριο Γαληνός

---

##### Lab 1: Περιβάλλον εργασίας

Για την υλοποίηση των εργασιών του εργαστηρίου θα πρέπει να εργαστείτε σε ένα Unix/Linux terminal. Θα ξεκινήσουμε με ένα περιβάλλον εργασίας σε μια διαθέσιμη διανομή (πχ ubuntu) και αργότερα θα εργαστείτε στην εγκατάσταση ενός λειτουργικού από τον πηγαίο κωδικά του.  

Θα αξιοποιήσετε κάποιες από τις ήδη διαθέσιμες εντολές του shell, αλλά θα χρειαστεί να εγκαταστήσετε και κάποια νέα προγράμματα.

Θα εργαστείτε καθένας στο δικό του περιβάλλον εκτέλεσης και θα πρέπει να εξοικειωθείτε με τον τρόπο που σας εξυπηρετεί καλύτερα.
Απότερος σκοπός είναι να δουλέψετε σε ένα σύστημα linux χωρίς systemd, όπως αναφέρουν οι οδηγίες του μαθήματος (https://courses-ionio.github.io/projects/dokey/).
_Πριν όμως καταφέρετε να κάνετε αυτό_ μπορείτε να επιλέξετε μπορείτε να αξιοποιήσετε μία από τις πιο κάτω _use your own device_ επιλογές:
 * Αξιοποίηση ενός _reusable & disposable_ **linux docker container**, _οδηγίες πιο κάτω_
 * Ήδη εγκατεστημένο linux, πχ ως dual boot, όποια διανομή σας βολεύει/αρέσει
 * Εγκατάσταση ενός linux εντός virtual box
 * Χρήση _persistent live ubuntu usb_ (επιτρέπει την εκτέλεση XUbuntu Desktop περιβάλλοντος το οποίο διατηρεί τις αλλαγές που κάνετε, πχ εγκατάσταση προγραμμάτων)
   - Ακουλουθήστε [αυτές](https://www.howtogeek.com/howto/14912/create-a-persistent-bootable-ubuntu-usb-flash-drive/) τις οδηγίες και δημιουργήστε το δικό σας persistent live usb (αρκεί ένα usb flash drive 8GB, προτείνεται __USB3__)

   _linux = όποια διανομή σας βολεύει/αρέσει_

###### Οδηγίες αξιοποίησης docker container

Εγκαταστήστε στο συστημά σας το [docker](https://www.docker.com/).
* Ξεκινήστε ένα `container` βασισμένο πχ στο Ubuntu 20.04 `image`, μελετήστε [εδώ](https://www.docker.com/resources/what-container) τη διαφορά/σχέση images-containers:  
`docker run --name ionio-sw-lab-2022 -it -p 8080:4000 ubuntu:20.04`
    * Η παράμετρος `--name` ονοματίζει τον container ώστε να μπορούμε να το σταματήσουμε/ξεκινήσουμε εύκολα διατηρώντας της αλλαγές που κάνουμε
    * Η παράμετρος `-it` εξασφαλίζει ότι ο container, αφού δεν το ζητάμε να εκτελέσει κάποια εντολή ή πρόγραμμα, δεν θα τερματιστεί με την ολοκλήρωση της εντολής
    * Η παράμετρος `-p` κάνει port mapping από το 8080 του μηχανήματός μας στο 4000 εντός του νέου container... τώρα δε μας χρειάζεται, αλλά θα το βρούμε μπροστά μας ;-)
    * Η διανομή που ξεκινάμε είναι `ubuntu` έκδοση `20.04`
    * _Tip_ Εκτελέστε σε ένα άλλο terminal την εντολή `docker ps` για να επιβεβαιώσετε ότι ο container σας τρέχει, να δείτε το container id του και το όνομά του:
    ```
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
    16a2dc0d7c03        ubuntu:20.04        "/bin/bash"         About an hour ago   Up About an hour                        ionio-sw-lab-2022
    ```

* Λογικά είστε ήδη εντός του container `ionio-sw-lab-2022`, αν για κάποιο λόγο δεμ είστε, συνδεθείτε στον container σας για να ξεκινήσουμε να δουλεύουμε εντός αυτού.  
`docker attach ionio-sw-lab-2022`  
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
    16a2dc0d7c03        ubuntu:20.04        "/bin/bash"         About an hour ago   Exited (0) 2 minutes ago                       ionio-sw-lab-2022
    ```

* Ξεκινάμε, πάλι:  
```docker start ionio-sw-lab-2022```  
και συνδεόμαστε στον container:  
```docker attach ionio-sw-lab-2022```  
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

##### Lab2: CV (Jekyll)

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
            * Από το pc μας, τώρα θα αξιοποιηθεί η παράμετρος `-p 8080:4000` που είχαμε δώσει όταν δημιουργήσαμε τον container. Η παράμετρος αυτή ενεργοποιεί port mapping από το host λειτουργικό μας προς τον container, άρα ό,τι είναι προσβάσιμο στον container στο port 4000 θα είναι προσβάσιμο στο host λειτουργικό μας στο port 8080 (_αλλά όχι το αντίστροφο από τον container προς το host! δεν υπάρχει κάποια τρύπα ασφάλειας_).  
            Άρα πολύ απλά στο βασικό μας λειτουργικό, μέσα από ένα brower ανοίγουμε τη διεύθυνση http://localhost:8080 και βλέπουμε τη σελίδα που _servήρει_ το Jekyll.  

    * Τώρα ας ξεκινήσουμε να φτιάχνουμε ένα site που θα περιέχει το cv μας.
        * Νέο site.. = νέο folder για το project μας  
        `mkdir /workspace/cv` και ας μεταβούμε σε αυτό  
        `cd /workspace/cv`
        * Αρχικοποιούμε όπως πριν, δεν ξεχνάμε τα προκαταρκτικά βήματα (εντός του folder που φιλοξενεί το νέο site μας):
            * `bundle init`
            * Προσθήκη gem στο Gemfile
            * `bundler`
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
            * Εκτελούμε `bundle exec jekyll build`
            * Και... τρέχουμε το `jekyll serve --host 0.0.0.0 &` (αν τρέχει κάποιο άλλο jekyll, οπότε δεν θα τρέξει το νέο jekyll serve instance, κάντε το `kill` με βάση το PID του) ελέγχουμε και... βλέπουμε ένα site στο οποίο τα δεδομένα διαχωρίζονται από την εμφάνιση!
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
        * Αξιοποιούμε το bundler που εγκαταστήσαμε νωρίτερα, άρα `bundle init`
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
        * **upd.** Αν θέλουμε υποστήριξη σε ελληνικά (πχ στο vim)
            * Εκτέλεση
            ```
            echo "el_GR UTF-8" > /etc/locale.gen
            locale-gen el_GR.UTF-8         
            ```
            * Προσθήκη στο `/root/.bashrc` και source το ίδιο αρχείο για να ξαναφορτωθεί
            ```
            export LANG="el_GR.UTF-8"
            export LC_CTYPE="el_GR.UTF-8"
            export LC_NUMERIC="el_GR.UTF-8"
            export LC_TIME="el_GR.UTF-8"
            export LC_COLLATE="el_GR.UTF-8"
            export LC_MONETARY="el_GR.UTF-8"
            export LC_MESSAGES="el_GR.UTF-8"
            export LC_PAPER="el_GR.UTF-8"
            export LC_NAME="el_GR.UTF-8"
            export LC_ADDRESS="el_GR.UTF-8"
            export LC_TELEPHONE="el_GR.UTF-8"
            export LC_MEASUREMENT="el_GR.UTF-8"
            export LC_IDENTIFICATION="el_GR.UTF-8"
            export LANG=el_GR.UTF-8
            export LC_ALL=el_GR.UTF-8
            ```
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
                * **Προσοχή εδώ, το github πλεον δεν δέχεται password authentication, θα πρέπει να πάτε στο `Github.com > Settings > Developer settings > Personal access tokens` και να εκδόσετε ένα νέο token (που να τα κάνει όλα ή να κάνετε refine τις επιλογές πρόσβασης που παρέχετε) και αυτό το token θα είναι το password που θα χρησιμοποιείτε**  
            Με το push στο __github.com__ το site γινεται _build_ και ανεβαίνει και στο __github.io__ (Github Pages)!

**ToDo (σας, <ins>για αυτή την εβδομάδα</ins>):**
1. Δείτε ένα πιο πλήρες yml για CV [εδώ](https://github.com/mrzool/cv-boilerplate)  
2. Συμπληρώστε τα στοιχεία σας (ή τέλος πάντων αρκετά) στο `_data/details.yml` και δημιουργήστε το κατάλληλο `index.html` για την προβολή τους.
    * Τσεκάρετε τακτικά locally, όταν είστε ικανοποιημένοι ανεβάστε στο github με push
3. Φροντίστε για έχετε καταγράψει στο asciinema τη δουλεία σας
4. Κάντε commit την πρόοδό σας

---
##### Lab3 & 4: Github submodule

Θα αξιοποιήσουμε ένα έτοιμο CV project ως submodule το οποίο παράγει αυτόματα μια PDF έκδοση του CV μας.

* Προσθέτουμε ως submodule το repo `https://github.com/mrzool/cv-boilerplate` στο φάκελο του cv μας:  
```
$ /workspace/cv-2022-1 (master)$ git submodule add https://github.com/mrzool/cv-boilerplate _2pdf
Cloning into '/workspace/cv-2022-1/_2pdf'...
remote: Enumerating objects: 318, done.
remote: Counting objects: 100% (28/28), done.
remote: Compressing objects: 100% (20/20), done.
remote: Total 318 (delta 15), reused 17 (delta 8), pack-reused 290
Receiving objects: 100% (318/318), 822.81 KiB | 2.77 MiB/s, done.
Resolving deltas: 100% (190/190), done.
$ /workspace/cv-2022-1 (master)$ ls _2pdf/
details.yml  makefile  output.pdf  preview.png  README.md  template.tex
```
Ήδη το περιεχόμενο του submodule repo έχει προστεθεί στο φάκελό μας, αλλά υπάρχουν και dependencies που χρειάζονται:

* Εγκατάσταση tinytex (χρειάζεται; δοκιμάστε να το παραλείψετε):  
    ```
    cd ~
    apt install wget
    wget -qO- "https://yihui.org/tinytex/install-bin-unix.sh" | sh
    ```
    * Προσθήκη στο PATH  
    `vi` το αρχείο `~/.bashrc` και προσθήκη σε αυτό `export PATH=$PATH:$HOME/bin`
    * Εγκατάσταση xelatex  
    ```apt-get install texlive-xetex```
    * Χρήση `tlmgr` για εγκατάσταση απαιτούμενων latex packages
        * Για κάθε package εκτελέστε πχ `tlmgr install polyglossia`
        * Αν δε βρίσκετε το package, ψάξτε το `tlmgr search multicol`
    * Εγκατάσταση pandoc  
    ```apt install pandoc```

* Εντός του `/workspace/cv-2022-1/_2pdf` εκτελέστε `make`  
Η εντολή `make` ουσιαστικά εκτελεί: `pandoc details.yml -o output.pdf --template=template.tex --pdf-engine=xelatex`
    * _Τρέχει; Αν λείπει κάποιο font εκτελέστε `fc-list` για να δείτε τι fonts υπάρχουν διαθέσιμα και αντικαταστήστε το `mainfont` στο αρχείο `details.yml`_
    * Ελέγξτε το παραγόμενο pdf αρχείο μέσω ενός browser στο url: http://localhost:8080/_2pdf/output.pdf
        * Το βλέπετε; https://github.com/jekyll/jekyll/issues/55
        * Μεταφέρετέ το (με `mv` ή `cp`) κάπου που θα το βλέπετε
    * Αλλάξτε το περιεχόμενο του details.yml και ξαναδημιουργήστε το pdf (και ξαναμεταφέρετέ το)

* Δημιουργήστε ένα pdf με βάση τα _δικά_ σας δεδομένα τα οποία βρίσκονται στο αρχείο `/workspace/cv-2022-1/_data/details.yml` και το οποίο να βρίσκεται στο root folder του repo σας με όνομα αρχείο `cv.pdf`

* Κάντε `git add` και `commit` το `cv.pdf`, όχι το φάκελο `_2pdf` και κάντε push στο GitHub.
* Δείτε το pdf cv σας στο github pages.

**ToDo (σας, <ins>έχετε χρόνο μέχρι την 7η εβδομάδα</ins>):**
1. _Συγχρονίστε οπτικά την html και pdf έκδοση του cv σας.
    * Τσεκάρετε τακτικά locally, όταν είστε ικανοποιημένοι ανεβάστε στο github με push
2. Φροντίστε για έχετε καταγράψει στο asciinema τη δουλεία σας
3. Κάντε commit την πρόοδό σας

**Follow-up (του lab 3)**  βασισμένο στο https://github.com/courses-ionio/help/discussions/287#discussion-3912896  
Τι γίνεται εάν προσθέσουμε ως submodule κώδικα τον οποίο θέλουμε να αλλάξουμε και να κάνουμε commit. _Αν το submodule δεν είναι δικό μας repo, τότε το commit/push -όπως είναι λογικό- αποτυγχάνει :-(_  
Ας το δοκιμάσουμε:
1. Κάνουμε clone το repo που ήδη περιέχει ένα _ξένο_ submodule:
    ```
    # git clone https://github.com/riggas-ionio/cv-2022-1.git
    Cloning into 'cv-2022-1'...
    remote: Enumerating objects: 17, done.
    remote: Counting objects: 100% (17/17), done.
    remote: Compressing objects: 100% (12/12), done.
    remote: Total 17 (delta 2), reused 17 (delta 2), pack-reused 0
    Unpacking objects: 100% (17/17), 1.85 KiB | 52.00 KiB/s, done.
    ```

2. Ελέγχουμε το φάκελο του submodule ο οποίος είναι κενός.
    ```
    cd cv-2022-1
    ls -al
    total 28
    drwxr-xr-x 5 root root 4096 Mar  9 19:51 .
    drwxr-xr-x 9 root root 4096 Mar  9 19:51 ..
    drwxr-xr-x 8 root root 4096 Mar  9 19:51 .git
    -rw-r--r-- 1 root root   82 Mar  9 19:51 .gitmodules
    ```  
    Το submodule είναι _συνδεδεμένο_ με το repo μας, αλλά όταν κάνουμε clone το repo μας, ο κώδικας του submodule δεν κατεβαίνει.

3. Ας κατεβάσουμε τον κώδικα του submodule. Στον αρχικό φάκελο του repo μας:
    ```
    git submodule update --init
    ls -al _2pdf/
    total 368
    drwxr-xr-x 2 root root   4096 Mar  9 20:14 .
    drwxr-xr-x 5 root root   4096 Mar  9 19:51 ..
    -rw-r--r-- 1 root root     30 Mar  9 20:14 .git
    -rw-r--r-- 1 root root     11 Mar  9 20:14 .gitignore
    -rw-r--r-- 1 root root   6069 Mar  9 20:14 README.md
    -rw-r--r-- 1 root root   1366 Mar  9 20:14 details.yml
    -rw-r--r-- 1 root root    190 Mar  9 20:14 makefile
    -rw-r--r-- 1 root root  35914 Mar  9 20:14 output.pdf
    -rw-r--r-- 1 root root 299228 Mar  9 20:14 preview.png
    -rw-r--r-- 1 root root   2866 Mar  9 20:14 template.tex    
    ```

4. Δοκιμάζουμε να κάνουμε μια αλλαγή σε ένα από τα αρχεία του submodule (_το οποίο *δεν* είναι δικό μας repo_):
    ```
    cd _2pdf/
    vi details.yml
    git add details.yml
    git commit -m "Changed a file in (someone else's) submodule"
    [detached HEAD 3ebf9e1] Changed a file in submodule
     1 file changed, 1 insertion(+), 1 deletion(-)
    git push origin master
    Username for 'https://github.com': riggas-ionio
    Password for 'https://riggas-ionio@github.com':
    remote: Permission to mrzool/cv-boilerplate.git denied to riggas-ionio.
    fatal: unable to access 'https://github.com/mrzool/cv-boilerplate/': The requested URL returned error: 403
    ```  
    και βέβαια αποτυγχάνει το push σε ξένο repo!  
    Θα ήταν δόκιμο να κάνουμε pull request, αντί push, αφού το repo είναι ξένο.  
    Αν όμως _για κάποιο λόγο_ πρέπει να χρησιμοποιούμε ένα repo το οποίο περιέχει submodule και θέλουμε να κάνουμε και push στο submodule, δεν έχουμε παρά να _οικειοποιηθούμε_ κάνοντάς το fork και **αντικαθιστώντας** το _ξένο_ submodule με το _οικειομποιημένο_ (forked) submodule.

5. Σβύνουμε ό,τι κάναμε ως εδώ (το folder με το αρχικό clone)..  
    ```
    cd /workspace
    rm -rf cv-2022-1
    ```  
    και εκτελούμε πάλι τα βήματα 1 και 2.

6. (ή νέο 3) Σβύνουμε το φάκελο του submodule αλλά και ό,τι πληροφορία περιέχει το git για το submodule.
    ```
    git rm --cached _2pdf/
    rm -rf _2pdf/
    ```

7. Προσθέτουμε το δικό μας (οικειοποιημένο, forked) repo και το αποθηκεύουμε σε φάκελο όλοιο με αυτό που μόλις σβύσαμε:  
    ```
    git submodule add https://github.com/riggas-ionio/cv-boilerplate _2pdf
    ```  
    τα αρχεία κατεβαίνουν από το **δικό** μας repo, άρα ότι αλλαγές και εάν κάνουμε στο submodule μπορούμε να τις κάνουμε commit/push.. γιατί πολύ απλά είναι δικό μας repo!   
    **Αλλά** προσοχή:  
    **Αν..**  
    κάνετε αλλαγές σε αρχεία του submodule και τα κάνετε commit εντός του submodule, _αλλά δεν τα κάνετε push_  
    **και**  
    κάνετε commit και push το root φάκελο (που περιέχει το submodule), τότε στο github θα λείπει το commit του submodule που θα βρίσκεται ακόμη στο δίσκο σας,  
    **οπότε** θα βλέπετε `HTTP 404 Error` 😱.

---

##### Lab 5: CV + Netlify

Έχουμε ήδη αξιοποιήσει τις δυνατότητες που παρέχουν τα Github & Jekyll για continuous deployment σε Github pages.  
Τώρα θα αξιοποιήσουμε και τις δυνατότητες που παρέχει το [Netlify](https://www.netlify.com/) για serverless δημοσιοποίηση διαδικτυακού περιεχομένου.  

* Κάνετε εγγραφή στο [Netlify](https://www.netlify.com/) και ένα νέο site βασισμένο σε ένα [Git repository](https://www.netlify.com/blog/2015/10/28/a-step-by-step-guide-jekyll-3.0-on-netlify/).
    * Επιλέξτε ως Git provider το Github και (αναγκαστικά) δώστε τις εξουσιοδοτήσεις που ζητά - προσπαθήστε να δώσετε όσο λιγότερη πρόσβαση μπορείτε, πχ μόνο στο repo που θέλετε να φιλοξενήσετε στο Netlify.
    * Επιλέξτε το **repository** που θέλετε να προσθέσετε και ποιο **branch** περιέχει τον κώδικα που θα κάνετε deploy.  
    __N.B.:__ σε αυτό το branch θα πρέπει να κάνετε commit/push ώστε οι αλλαγές να κάνουν trigger το νέο deployment.
    * Δεδομένου ότι είναι jekyll based το site μας, δώστε τα κατάλληλα [basic build settings](https://docs.netlify.com/configure-builds/common-configurations/#jekyll):
        * Build command: `jekyll build`
        * Publish directory: `_site`  


:-) Τέλος... _καλό;_        
:-/ μπα..

* Μια συλλογή από σφάλματα που ίσως εμγανίζονται στο deploy log: (´･_･`)
    * Το Netlify δεν βρίσκει το jekyll...  
    * `GitHub Metadata: Error processing value 'title':`


* Επιβεβαιώστε ότι:
    * Στο github repository έχετε περιλάβει τα αρχεία `Gemfile` και `Gemfile.lock` που έχετε δημιουργήσει για να _βλέπετε_ τοπικά το jekyll based cv σας. Στο github αυτά δεν ήταν απαραίτητα, αφού ουσιαστικά τα είχαμε δημιουργήσει τοπικά για να κάνουμε replicate το setup του github/pages, τώρα είναι απαραίτητα στο Netlify, άρα κάνετε τα git add/commit/push.
    * Στο github repository έχετε περιλάβει ενα _config.yml αρχείο, πρόκειται για jekyll config file το οποίο στο github (πάλι) δεν ήταν απαραίτητο, αλλά για το Netlify χρειάζεται. Τα ελάχιστα δεδομένα που πρέπει να περιέχει είναι τιμή για το όνομα του `repository` που συνδέετε με το Netlify

Σε κάθε push που κάνετε στο github γίνεται πλέον αυτόματα trigger ένα deploy στο githib pages και ένα ακόμη στο Netlify.  
🌍🔋 __Think before you push__ (to the repo)! Test locally! Αν όχι για άλλο λόγο, γιατί το free account του Netlify σας δίνει 300 build minutes/month, άρα κάθε commit που δεν παράγει σωστό αποτέλεσμα είναι _(περιορισμένα) resources που πάνε χαμένα_.

**ToDo (σας, <ins>για αυτή την εβδομάδα</ins>):**  
* Εξερευνήστε περισσότερο το Netlify, πχ χαρίστε ένα πιο κομψό url στο site σας.

---

##### Lab 6: CV (Github pages + Netlify) + αυτόματη περίληψη του pdf cv σε κάθε commit.

Έχουμε ήδη δει πώς μπορούμε να πετύχουμε Continuous Deployment του html CV σε Github pages + Netlify. Πώς όμως μπορούμε να αυτοματοποιήσουμε τη διαδικασία και για τη PDF έκδοση του CV; Δλδ κάθε φορά που κάνουμε μια αλλαγή στο index.html ή στο details.yml και κάνουμε commit το pdf να δημιουργείται αυτόματα και να περιλαμβάνεται στο τελευταίο commit;

* Θα αξιοποιήσουμε [Git hooks](https://www.atlassian.com/git/tutorials/git-hooks)  τα οποία είναι _"scripts that run automatically every time a particular event occurs in a Git repository. They let you customize Git’s internal behavior and trigger customizable actions at key points in the development life cycle"_  
    * Σε κάθε git repo folder υπάρχει ένας κρυφός φάκελος, ο `.git/hooks`, ο οποίος περιέχει ποικίλα hook samples. Για κάθε sample hook το filename του δηλώνει πότε εκτελείται.
    * Χρησιμοποιήστε [αυτή](https://stackoverflow.com/questions/3284292/can-a-git-hook-automatically-add-files-to-the-commit/12802592#12802592) την τεχνική για να μπορέσετε να προσθέσετε ένα αρχείο (το `cv.pdf`) στο τελευταίο commit.
        * Για να έχετε πάντα διαθέσιμο το πιο επικαιροποιημένο `cv.pdf`, εντός του κατάλληλου git hook μπορείτε να παράγεται το `cv.pdf` χρησιμοποιώντας ό,τι κάνατε στο Lab 3 για την παραγωγή pdf από δεδομένα σε yaml μορφή και ένα προτυπο tex αρχείο.
    * Τροποποιήστε το `index.html` ώστε να περιέχει ένα link που να δείχνει στο `cv.pdf` αρχειο.

**ToDo (σας, <ins>για αυτή την εβδομάδα</ins>):**  
* Συνδυάστε όλα τα προηγούμενα ώστε σε κάθε commit να παράγεται νέο `cv.pdf` και αυτό να προστίθεται στο τελευταίο commit.
* Μπορείτε να κάνετε refine τη διαδικασία, ώστε νέο pdf να παράγεται (και συνεπώς να προστίθεται στο τελευταίο commit) μόνο εφόσον έχει υπάρξει αλλαγή σε αρχείο που επηρεάζει το `cv.pdf` (πχ στο yaml ή το tex αρχείο); Γιατί να σπαταλάτε processing resources εάν απλά έχει αλλάξει η γραμματοσειρά πχ στο `index.html`;

---

##### Lab 7: CV + Continuous Integration και user notifications

Δε θα ήταν καλά να είχαμε (όπου προτιμούμε.. στην κινητή μας συσκευή, στο laptop/desktop μας) ειδοποιήσεις οποτεδήποτε συμβαίνει κάτι ενδιαφέρον, πχ γίνεται commit μια νέα έκδοση του cv μας;

* Εγκαταστήστε το `ntfy` (αρκεί `pip3 install ntfy`) και (αρχικά) κάνετε το απαραίτητο configuration για να στέλνει τις ειδοποιήσεις του στο syslog του συστήματός σας.
     - Βεβαιωθείτε ότι το `/var/log/syslog` υπάρχει και ενημερώνεται. Αν όχι, βεβαιωθείτε για την εγκατάσταση του σχετικου deamon με την εντολή `sudo apt-get install --reinstall rsyslog` και στη συνέχεια βεβαιωθείτε για την ενεργοποίησή του με την εντολή `sudo service rsyslog restart`.
     - Ελέγξτε ότι το syslog γράφεται, εκτελέστε την εντολή `logger Hello logger service!` (δεν χρεάζεται quotes) και ελέγξτε ότι γράφτηκε το μήνυμα στο αρχείο syslog με την εντολή `tail /var/log/syslog`.
     - Ελέγξτε ότι έχει εγκατασταθεί το (σε λίγο) απαραίτητο python module `syslog-py`.
* Κάνετε configure το ntfy (δημιουργήστε ή ενημερώστε το `~/.ntfy.yml` αρχείο σας) ώστε να στέλνει τις ειδοποιήσεις του στο syslog (_Seriously τώρα.. ο μόνος λόγος που το στέλνουμε στο syslog είναι για να το κάνετε asciinema_:-).
* Επιλέξτε ένα άλλο backend για να προωθεί το `ntfy` τις ειδοποιήσεις. Στο φάκελο `/usr/local/lib/python3.8/dist-packages/ntfy/backends/` (ή κάτι ανάλογο, αναλόγως της έκδοσης python που τρέχετε και του λειτουργικού σας) υπάρχουν ποικίλα backends τα οποία μπορείτε να ενεργοποιήσετε.
    * _Ή ακόμη καλύτερα να χρησιμοποιήσετε ως πρότυπα για να φτιάξετε ένα δικό σας!_

**ToDo (σας, <ins>για αυτή την εβδομάδα</ins>):**  
* Επεξεργαστείτε τα git hooks της περασμένης εβδομάδας έτσι ώστε όποτε γίνεται commit μια νέα έκδοση του `cv.pdf` να λαμβάνετε μια ειδοποίηση από το `ntfy`.
* Αξιοποιήστε το μηχανισμό [slack incoming webhooks](https://api.slack.com/legacy/custom-integrations/messaging/webhooks) ώστε να λαμβάνεται τις ειδοποιήσεις σας σε ένα channel εντός ενός workspace σας.

---

##### Lab 8: CV + Continuous Integration και MQTT notifications

Δημιουργήστε ένα (free) account στο https://ide.goorm.io/. Δημιουργήστε ένα container βασισμένο σε python.  
Μόλις αποκτήσατε ένα cloud based linux machine ;-). Ξεκινάμε..  

* Εγκαταστήστε το [mosquitto](https://mosquitto.org/) ένα mqtt broker: `apt-get install mosquitto`
    * Τρέχει;... δοκιμάστε: `/etc/init.d/mosquitto status`, αν το αποτέλεσμα είναι  
    `mosquitto is not running`  
    ελέγξτε το logging που έγινε κατά την εγκατάσταση.
    Αν αναφέρει  
    `invoke-rc.d: policy-rc.d denied execution of start.`  
    τότε εκτελέστε:  
    ```
    printf '#!/bin/sh \n exit 0' > /usr/sbin/policy-rc.d
    /etc/init.d/mosquitto start
    /etc/init.d/mosquitto status
    ```
    και το πρόβλημα πρέπει να λύθηκε, αν όχι _google it!_
* Εγκαταστήστε και αντίστοιχους clients:  
`apt-get install mosquitto-clients`
    * Δοκιμάστε... `mosquitto_sub -t "notifications" &`
    και.. `mosquitto_pub -m "Hello World from mosquitto_pub client" -t "notifications"`  
    Εμφανίστηκε το μήνυμα; Όλα καλά, αλλιώς.. _debug it!_

* Εγκαταστήστε το [mqttwarn](https://github.com/jpmens/mqttwarn):
    ```
    pip3 install --upgrade
    pip3 install mqttwarn
    ```
    * Δημιουργήστε και μεταβείτε σε ένα φάκελο `/workspace/mqttwarn`
    * Ακολουθήστε τα βήματα του configuration που περιγράφονται:  
    ```
    # Create configuration file
    mqttwarn make-config > mqttwarn.ini

    # Create file for custom functions
    mqttwarn make-samplefuncs > samplefuncs.py
    ```
    * Προσθέστε το config τις απαραίτητες ρυθμίσεις για το [http](https://github.com/jpmens/mqttwarn/blob/master/HANDBOOK.md#http).
        * Τροποποιήστε κατάλληλα το post action ώστε να κάνει post στο url του slack api endpoint σας.  
        Σημεία στο αρχείο init που χρειάζεται να <u>παρέμβετε</u> (_μην καταργήσετε συνολικά το .ini αρχείο_) είναι τα:
        ```
        ; name the service providers you will be using.
        launch    = file, log, http

        ; -------
        ; Targets
        ; -------

        [config:http]
        timeout = 60
        targets = {
                        #method     #URL               # query params or None                              # list auth # Json
          'notifications'    : [ "post", "https://hooks.slack.com/services/___/___/___", None, True ]
          }

        ; ------------------------------------------
        ;                  Basic
        ; ------------------------------------------

        [hello/1]
        ; echo '{"name": "temperature", "number": 42.42}' | mosquitto_pub -h localhost -t hello/1 -l
        targets = log:info
        format = u'{name}: {number} => {_dthhmm}'

        [notifications]
        targets = http
        ```    
        Χρησιμοποιήστε το slack hook της περασμένης εβδομάδας.    
    * Ίσως χρειαστεί λίγο debugging ο κώδικας του http module :-)  
    Αν παρατηρήσετε τα logging νημύματα του mqttwarn προκύπτει σφάλμα κατά την εκτέλεση του αρχείο `/usr/local/lib/python3.8/dist-packages/mqttwarn/services/http.py`: ***'Request' object has no attribute 'add_data'***.  
    Κάνετε edit το αρχείο τροποποιώντας τη γραμμή:  
    `#request.add_data(encoded_params)` σε  
    `request.data = bytes(encoded_params, 'utf-8')`  
    Αν κάνετε publish στο mosquitto ένα json το οποίο αποδέχεται το slack, θα πρέπει να δείτε το μήνυμά σας στο slack.  
    Αν το μήνυμα δεν είναι κατάλληλα μορφοποιημένο για το slack, θα βλέπετε στο mqttwarn log ***HTTP Error 400: Bad Request***, αρκεί να στείλετε ένα ορθό json formatted μήνυμα στο hook.    

**ToDo (σας, <ins>για αυτή την εβδομάδα</ins>):**  
* Επεξεργαστείτε τα git hooks της περασμένης εβδομάδας έτσι ώστε όποτε γίνεται commit μια νέα έκδοση του `cv.pdf` να στέλνετε ένα mqtt message στο mosquitto που τρέχει στο goorm container σας και από εκεί να γίνεται κατάλληλη μορφοποίηση και προώθηση στο slack webhook σας.  
Ο goorm container σας είναι προσβάσιμος μέσω url που μπορείτε να βρείτε στο μενού `PROJECT > Running URL and Port`. Βρείτε σε port _ακούει_ ο mqtt broker και αν αυτό δεν είναι προσβάσιμο (ανοιχτό) φροντίστε να γίνει, αν χρειαστεί αξιοποιήστε το μηχανισμό `CONTAINER > Port Forwarding Configuration`.

* :fireworks: Αφού δεν υπάρχει module για το slack api (που να δουλεύει με webhook)... γιατί δε φτιάχνετε ένα; _λίγη αλλαγή το module http απαιτείται μόνο!_  
:fireworks: :fireworks: Αφού το φτιάξετε, γιατί δεν το ανεβάζετε και στο github! Κάντε και ένα pull request στο mqttwarn και ίσως γίνετε μέρος του δημόσιου ανοιχτού λογισμικού! :-)

---

##### Lab 9: Terminal multiplexing: doing more than one thing on a single terminal

Εγκαταστήστε το tmux ακολουθώντας τις οδηγίες: https://linuxize.com/post/getting-started-with-tmux/.  
Το tmux σας δίνει τη δυνατότητα να έχετε πολλαπλά terminal sessions στο ίδιο παράθυρο.  

* Ξεκινήστε το tmux εντός ενός terminal σας εκτελώντας `tmux`. Δημιουργήθηκε ένα νέο session από το οποίο μπορείτε να εξέλθετε χωρίς να τερματιστεί με `Ctrl+b` `d`.
* Από το βασικό σας terminal (εκτός του tmux) δημιουργήστε ένα νέο session με ονομασία `tmux new -s goorm`.
    * Εντός του νέου session, συνδεθείτε στο goorm container της περασμένης εβδομάδας. Οδηγίες σύνδεσης στο μενού του Goorm: `CONTAINER > SSH Configuration`, όπου θα δημιουργήσετε ssh password.
* Αξιοποιήστε το (ένα, μοναδικό) terminal παράθυρό σας για να εργαστείτε παράλληλα στο τοπικό μηχάνημά σας και στο goorm ssh session σας με εναλλαγή μεταξύ των tmux sessions.
* Εξερευνήστε plugins τα οποία σας επιτρέπουν να κάνετε save και restore τα tmux sessions. 
