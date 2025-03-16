# Ansible !

--> SLIDE 1

![image info](./imgs/ansible_inv_start.svg)

Ansible e' un sistema di "configuration management", composto da un "control node" che 
tramite dei "playbooks", applicati contro dei "managed nodes" presenti nell' "inventory",
gli fa eseguire dei compiti.

Gli scopi di questo sistema sono quelli di:
    - eliminare le ripetizioni e semplificare il flusso di lavoro
    - gestire e mantenere la configurazione dei sistemi
    - permettere il deployment di software complesso
    - eseguire "rolling updates" a zero downtime

Include una architettura agentless, tipica dei sistemi RHEL ( podman ), e' estremamente semplice da usare,
flessibile e scalabile, predicibile e ( finalmente ) equipollente.  

Red Hat® Ansible Automation Platform è stato realizzato con gli stessi elementi base della versione di Ansible sviluppata dalla community. La differenza è che offre un supporto completo di livello enterprise durante l'intero ciclo di vita e include caratteristiche progettate per aiutare le organizzazioni a standardizzare, ridimensionare e rendere operativa l'automazione. 

## L’Impatto dell’Infrastructure Automation sugli Operatori IT (DevOps)
L’infrastructure automation rappresenta una delle evoluzioni più significative nel panorama IT degli ultimi anni. Si tratta di un approccio che consente di gestire e configurare infrastrutture IT attraverso codice e strumenti automatizzati, riducendo l’intervento manuale e migliorando l’efficienza complessiva. Per gli operatori IT, in particolare per i team DevOps, questa trasformazione ha avuto un impatto profondo, ridefinendo ruoli, competenze e modalità operative.

### Riduzione delle attività ripetitive
Tradizionalmente, molte attività nell’amministrazione dei sistemi erano manuali, come la configurazione di server, il provisioning delle risorse o il monitoraggio dei sistemi. Con strumenti di automation come Terraform, Ansible, Puppet o Chef, queste attività vengono automatizzate, liberando gli operatori IT da compiti ripetitivi e soggetti a errori. Questo consente ai team DevOps di concentrarsi su attività a maggiore valore aggiunto, come l’ottimizzazione delle architetture o lo sviluppo di nuove funzionalità.

### Accelerazione dei processi DevOps
Uno degli obiettivi chiave del DevOps è ridurre i tempi di rilascio del software, migliorando al contempo la qualità delle applicazioni. L’infrastructure automation facilita questo processo, rendendo possibile il provisioning e la configurazione rapida e coerente degli ambienti. Ad esempio, l’utilizzo di script Infrastructure as Code (IaC) permette di creare ambienti di sviluppo, test e produzione identici, eliminando problemi legati a configurazioni incoerenti.

### Crescita delle competenze tecniche
Per gli operatori IT, l’automazione dell’infrastruttura richiede un aggiornamento significativo delle competenze. La padronanza di strumenti come Terraform o Ansible, la conoscenza dei linguaggi di scripting (come Python o YAML) e la comprensione delle architetture cloud sono diventate competenze essenziali. Inoltre, l’approccio DevOps spinge gli operatori IT a collaborare strettamente con i team di sviluppo, acquisendo competenze in settori tradizionalmente separati, come il versionamento del codice o l’integrazione continua.

### Maggiore resilienza e affidabilità
L’automazione consente di implementare configurazioni standardizzate e ripetibili, riducendo la possibilità di errori umani. Questo migliora la resilienza dei sistemi e la loro capacità di recupero in caso di guasti. Inoltre, gli strumenti di automation integrano spesso funzionalità di audit e logging, garantendo una maggiore trasparenza e tracciabilità delle modifiche, un aspetto fondamentale per la compliance e la sicurezza.

### Implicazioni per il ruolo degli operatori IT
L’automazione sta trasformando il ruolo degli operatori IT. In passato, gran parte del lavoro era dedicata al mantenimento e al supporto delle infrastrutture. Oggi, gli operatori IT sono sempre più coinvolti nella progettazione di sistemi scalabili e nell’implementazione di pipeline automatizzate. Il risultato è un ruolo più strategico e orientato all’innovazione.

### Sfide e opportunità
Sebbene l’automazione porti numerosi vantaggi, presenta anche sfide. Gli operatori IT devono affrontare una curva di apprendimento iniziale e la complessità di gestire strumenti eterogenei. Inoltre, l’adozione dell’automazione richiede un cambiamento culturale, in cui il fallimento è considerato parte del processo di miglioramento continuo. Tuttavia, le opportunità sono immense: maggiore efficienza, scalabilità e un ruolo professionale più dinamico e stimolante.

### Conclusione
L’automazione dell’infrastruttura non è solo una tendenza tecnologica, ma una trasformazione che ridefinisce il modo in cui i team IT operano. Per i professionisti DevOps, rappresenta una sfida e un’opportunità unica per evolvere, acquisire nuove competenze e contribuire in modo strategico al successo delle organizzazioni. Il futuro del settore sarà sempre più legato alla capacità di abbracciare l’automazione e di sfruttarla per creare sistemi più resilienti, agili e innovativi.

### Configuriamo l'ambiente

### Installare

    https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170#latest-microsoft-visual-c-redistributable-version
    https://download.virtualbox.org/virtualbox/7.0.18/VirtualBox-7.0.18-162988-Win.exe
    https://developer.hashicorp.com/vagrant/install?product_intent=vagrant
    https://download.mobatek.net/2412024041614011/MobaXterm_Installer_v24.1.zip
    https://winscp.net/download/WinSCP-6.3.5-Setup.exe/download


## Installiamolo su Debian
```
sudo apt install wget gpg
UBUNTU_CODENAME=jammy
wget -O- "https://keyserver.ubuntu.com/pks/lookup?fingerprint=on&op=get&search=0x6125E2A8C77F2818FB7BD15B93C4A3FD7BB9C367" | sudo gpg --dearmour -o /usr/share/keyrings/ansible-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/ansible-archive-keyring.gpg] http://ppa.launchpad.net/ansible/ansible/ubuntu $UBUNTU_CODENAME main" | sudo tee /etc/apt/sources.list.d/ansible.list
sudo apt update -y && sudo apt install ansible -y
ansible-config init --disabled -t all > /etc/ansible/ansible.cfg_NO
```

### YAML

-> Che cos'è un file YAML? 
Il file YAML è costituito da un linguaggio YAML (YAML Ain’t Markup Language) che è un linguaggio di
serializzazione dei dati basato su Unicode; utilizzato per i file di configurazione, la messaggistica Internet,
la persistenza degli oggetti, ecc. YAML utilizza l’estensione .yaml per i suoi file. La sua sintassi è indipendente
da un linguaggio di programmazione specifico. Fondamentalmente, YAML è progettato per l’interazione umana e per
funzionare bene con i moderni linguaggi di programmazione. Il supporto per la serializzazione di strutture dati
native arbitrarie ha aumentato la leggibilità dei file YAML, ma ha reso un po’ complicato il processo di analisi
e generazione dei file.

--> Breve storia 
YAML è stato proposto per la prima volta nel 2001 ed è stato sviluppato da Clark Evans, Ingy döt Net e Oren Ben-Kiki.
Inizialmente si diceva che YAML significasse “Ancora un altro linguaggio di markup” per indicare il suo scopo come
linguaggio di markup. Successivamente è stato riproposto come “YAML Aint Markup Language” per indicare il suo scopo
come orientato ai dati.

--> Formato file YAML 
Il file YAML è costituito dai seguenti tipi di dati

Scalari: gli scalari sono valori come stringhe, numeri interi, booleani, ecc.
Sequenze: le sequenze sono elenchi con ogni elemento che inizia con un trattino (-). Gli elenchi possono anche essere nidificati.
Mappatura: la mappatura offre la possibilità di elencare chiavi con valori.

--> Sintassi 
Spazi bianchi: il rientro degli spazi bianchi viene utilizzato per indicare l’annidamento e la struttura generale.
```
nome: John Smith
contatto:
casa: 1012355532
ufficio: 5002586256
indirizzo:
strada: |
123 vicolo Tornado
Suite 16
città: East Centerville
stato: KS
```

Commenti: i commenti vengono scritti iniziando con il simbolo “#”.
```
# Questo è un commento YAML
```

Elenchi: il trattino (-) viene utilizzato per indicare i membri dell’elenco con ciascun membro su una riga separata.
I membri dell’elenco possono anche essere racchiusi tra parentesi quadre ([…]) con i membri separati da virgole (,).
```
  - A
  - B
  - C
```
```
[A, B, C]
```
Matrice associativa: una matrice associativa è racchiusa tra parentesi graffe ({…}).
Le chiavi e i valori sono separati da due punti(:) e ogni coppia è separata da virgola (,).
```
{name: John Smith, age: 20}
```
Stringhe: la stringa può essere scritta con o senza virgolette doppie (") o virgolette singole (’).
```
Esempio di stringa
"Stringa campione"
'Stringa campione'
```
Contenuto del blocco scalare: il contenuto scalare può essere scritto in notazione a blocchi utilizzando quanto segue:
      - |: All live breaks are significant.
      - >: Each line break is folded to space. It removes the leading whitespace for each line.
```
```
Documenti multipli: più documenti sono separati da tre trattini (—) in un unico flusso.
I trattini indicano l’inizio del documento. I trattini vengono utilizzati anche per separare le direttive dal contenuto del documento.
La fine del documento è indicata da tre punti (…).
```
  ---
Documento 1
  ---
Documento 2
...
```
Tipo: per specificare il tipo di valore, vengono utilizzati i doppi punti esclamativi (!!).
```
a: !! galleggiante 123
b: !!str 123
```
Tag: per assegnare un tag a una nota, viene utilizzata una e commerciale (&) e per fare riferimento a quel nodo, viene utilizzato un asterisco (*).
```
nome: John Smith
fattura a: &id01
strada: |
123 vicolo Tornado
Suite 16
città: East Centerville
stato: KS

spedizione a: *id01
```

Direttive: i documenti YAML possono essere preceduti da direttive in un flusso.
Le direttive iniziano con un segno di percentuale (%) seguito dal nome e poi dai parametri separati da spazi.

```
%YAML 1.2
  ---
Contenuto del documento
```

Esempio di file YAML 
Qui puoi vedere un esempio di file yaml docker di seguito:

```
topology:
database_node_name: docker_controller
docker_controller_node_name: docker_controller
self_service_portal_node_name: docker_controller
kvm_compute_node_names: kvm_compute1
docker_compute_node_names: docker_compute1
```


--> YAML vs JSON 
Fondamentalmente, sia JSON che YAML sono sviluppati per fornire un formato di interscambio di dati leggibile dall’uomo.
YAML è realizzato come un superset del formato JSON.
Significa che possiamo analizzare JSON usando un parser YAML.
Sebbene l’implementazione pratica di questa teoria sia poco complicata.
Pertanto, alcune differenze di base tra YAML e JSON sono riportate di seguito:

|YAML	 | JSON |
| :--- | :--- |
|Processo complesso e dispendioso in termini di tempo per l’analisi dei dati serializzati	| Analizza i dati serializzati JSON in modo rapido e semplice grazie al suo design più semplice
|Meno supporto della comunità	| Supporto e popolarità della community più ampia |
|Supporta i commenti |	Non supporta i commenti |
|Possibilità di utilizzare il riferimento di altri oggetti di dati | 	Impossibile serializzare strutture complesse con riferimenti a oggetti |
|La gerarchia è indicata utilizzando caratteri a doppio spazio. I caratteri di tabulazione non sono consentiti |	Gli oggetti e gli array sono indicati tra parentesi graffe e parentesi quadre. |
|Le virgolette delle stringhe sono facoltative ma supportano le virgolette singole e doppie. | Le stringhe devono essere racchiuse tra virgolette doppie. |
|Il nodo radice può essere uno qualsiasi dei tipi di dati validi |	Il nodo radice deve essere un array o un oggetto |

## Use case
Abbiamo scritto uno script che configura tre webservers.
In ansible gli script si chiamano `playbook` e le macchine su cui dobbiamo eseguire i nostri scripts 
sono i `remote hosts`.

Diciamo che l'obiettivo dei nostri playbooks sia quello di installare nginx, generare un file di configurazione, copiare i certificati 
di sicurezza e avviare il servizio nginx.

Il tutto verra' eseguito con il comando 
`ansible-playbook webservers.yml`
Ansible creera' una connessione ssh, senza agente e quindi, usando il solo server sshd sulla macchina remota, ed eseguira' in ordine
i task presenti nel playbook 

Il nostro primo task del playbook sara' qualcosa di molto simile:

```
    - name: install nginx
    apt: name=nginx
```

Ansible generera' uno script python che installi il webserver e lo copiera' su tutti e tre i server remoti, lo eseguira' localmente ed
aspettera' che l'esecuzione sia completata. Questo avverra' per ogni task che gli abbiamo detto di eseguire.

Bisogna tenere presente che:

  - Gli script vengono eseguiti in parallelo su tutti gli host remoti,
  - ansible aspetta che un task sia stato completato ( ritorni un exit status ) 
    su tutte le macchine
  - ansible rispetta la sequenza dei task impostata dallo sviluppatore

![image info](./imgs/ansible_deployment.png)  

## Gli inventory

creiamo le cartelle necessarie

```
mdkir -p ./ansible/inventory ./ansible/playbooks ./ansible/roles
```

```
--> .ini

cat > /etc/ansible/hosts << EOF
[test]
remote_host ansible_ssh_host=10.0.0.12 ansible_ssh_port=22
pippo 10.0.0.10
EOF

--> yaml
cat > /etc/ansible/hosts << EOF
myhosts:
  hosts:
    remote_host:
      ansible_host: 10.0.0.12
      ansible_ssh_port: 22
EOF
```

```
ansible-inventory -i /etc/ansible/hosts --list
ansible myhosts -m ping -i /etc/ansible/hosts
```

Inventory complesso possono essere scritti come segue:

```
leafs:
  hosts:
    leaf01:
      ansible_host: 192.0.2.100
    leaf02:
      ansible_host: 192.0.2.110

spines:
  hosts:
    spine01:
      ansible_host: 192.0.2.120
    spine02:
      ansible_host: 192.0.2.130

network:
  children:
    leafs:
    spines:

webservers:
  hosts:
    webserver01:
      ansible_host: 192.0.2.140
    webserver02:
      ansible_host: 192.0.2.150

datacenter:
  children:
    network:
    webservers:
```

Testiamo la nostra configurazione:
`ansible test -i /etc/ansible/hosts -m ping -vvvvv`

LAB!! 

--> scrivere un inventory con notazione yaml della macchina remota
con tre diverse notazioni ( ma stesso IP ) webserver, db e fileserver 

## Organizzazione di un Delivery tramite il File ansible.cfg
Il file ansible.cfg è uno degli elementi centrali per configurare e organizzare un delivery efficace con Ansible. È un file di configurazione che consente di personalizzare e ottimizzare il comportamento di Ansible durante l'esecuzione dei playbook e delle attività automatizzate. La sua corretta configurazione è fondamentale per gestire ambienti complessi e migliorare l'efficienza operativa.

Ecco come è strutturato e utilizzato il file ansible.cfg per organizzare un delivery:

1. Struttura del File ansible.cfg
Il file ansible.cfg è diviso in sezioni predefinite, ognuna dedicata a un particolare aspetto del funzionamento di Ansible. Alcune delle sezioni più comuni includono:

[defaults]
Questa è la sezione principale per le impostazioni generali. Contiene configurazioni che si applicano a tutte le operazioni di Ansible, a meno che non siano sovrascritte in specifiche attività o playbook.

Esempio:
```
[defaults]
inventory = ./inventory/hosts.ini
remote_user = ansible_user
private_key_file = ~/.ssh/id_rsa
host_key_checking = False
retry_files_enabled = False
forks = 10
```
inventory: Specifica il file di inventario utilizzato.
remote_user: L'utente remoto predefinito per le connessioni.
private_key_file: Percorso della chiave privata SSH.
host_key_checking: Disabilita il controllo della chiave host per evitare errori in ambienti dinamici.
retry_files_enabled: Disattiva la creazione di file .retry (utile per evitare confusione nei workflow CI/CD).
forks: Numero di processi paralleli che Ansible può eseguire.
[inventory]
Configura il comportamento dell'inventario.
```
[inventory]
enable_plugins = yaml, ini, script
```
enable_plugins: Specifica i plugin di inventario abilitati, come YAML o script dinamici.
[privilege_escalation]
Definisce le impostazioni per l'escalation dei privilegi (ad esempio sudo).
```
[privilege_escalation]
become = True
become_method = sudo
become_user = root
become_ask_pass = False
```
become: Abilita l’uso di sudo o altri metodi di escalation.
become_method: Metodo di escalation (es. sudo, su).
become_user: Utente di destinazione per l’escalation.
[ssh_connection]
Configura le impostazioni per la connessione SSH.
```
[ssh_connection]
pipelining = True
ssh_args = -o ControlMaster=auto -o ControlPersist=60s
```
pipelining: Migliora le prestazioni riducendo i comandi SSH eseguiti separatamente.
ssh_args: Specifica opzioni avanzate per le connessioni SSH.
[callback_plugins]
Consente di configurare plugin per la visualizzazione e il logging.
```
[callback_plugins]
stdout_callback = yaml
```
2. Organizzazione del Delivery
Per organizzare un delivery efficiente, il file ansible.cfg deve essere integrato in una struttura di progetto coerente. Un esempio di struttura potrebbe essere:
```
project/
├── ansible.cfg
├── inventory/
│   ├── hosts.ini
│   ├── group_vars/
│   │   └── all.yml
│   └── host_vars/
│       └── server1.yml
├── playbooks/
│   ├── deploy.yml
│   ├── update.yml
│   └── rollback.yml
├── roles/
│   ├── webserver/
│   │   ├── tasks/
│   │   │   └── main.yml
│   │   ├── templates/
│   │   │   └── nginx.conf.j2
│   │   └── vars/
│   │       └── main.yml
│   └── database/
└── files/
    └── app.war
```
Centralizzazione delle Configurazioni: Collocare il file ansible.cfg nella directory principale del progetto per applicare le configurazioni a tutti i playbook e ruoli.
Gestione delle Variabili: Usare group_vars e host_vars per definire variabili specifiche per gruppi o host.
Separazione dei Ruoli: Organizzare i ruoli in directory dedicate per facilitare il riutilizzo e la modularità.

3. Best Practices
Versionamento: Includere il file ansible.cfg nel controllo di versione (es. Git) per garantire consistenza tra gli ambienti.
Sicurezza: Evitare di memorizzare credenziali sensibili nel file; utilizzare strumenti come Ansible Vault.
Ottimizzazione: Abilitare pipelining e aumentare il valore di forks per migliorare le prestazioni.
Personalizzazione: Configurare plugin di callback e log per una migliore visibilità dei processi.
Un file ansible.cfg ben configurato è essenziale per un delivery efficiente, riducendo errori e migliorando la scalabilità delle operazioni.

Consideriamo pero' che il .cfg puo' essere posizionato, per motivi diversi, in posizioni diverse.
Automaticamente Ansible lo cerchera':
1. nella posizione speficicata dalla variabile d'ambiente ANSIBLE_CONFIG
2. ./ansible.cfg
3. ~/.ansible.cfg
4. /etc/ansible/ansible.cfg

### Le variabili

Le variabili lsi possono applicare ad ogni istanza di "managed nodes", anche i gruppi
```
webservers:
  hosts:
    webserver01:
      ansible_host: 192.0.2.140
      http_port: 80
    webserver02:
      ansible_host: 192.0.2.150
      http_port: 443
  vars:
    ansible_user: my_server_user
```

## I playbooks

### Hello world

```
cat > 
- name: My first play
  hosts: myhosts
  tasks:
   - name: Ping my hosts
     ansible.builtin.ping:

   - name: Print message
     ansible.builtin.debug:
       msg: Hello world
```

```
ansible-playbook -i inventory.ini playbook.yaml
```

LAB!!
--> scrivi un playbook che pinghi un host remoto e uno che stampi a 
    monitor un messaggio a tua scelta

## I moduli
LAB!
scrivi un plabook con un task per ogni modulo spiegato finora.

## task handlers

Gli Handlers sono istruzioni che vanno eseguite come conseguenza di una determinata azione. Ad esempio dopo l’installazione di una applicazione potremmo voler avviare il servizio.
I Playbook sono insiemi di Tasks e Handlers. Un esempio di playbook potrebbe essere quello per l’installazione e la configurazione di un sistema Apache, php e mysql, che comprende vari step da eseguire in sequenza.

## Loop e Condizionali
LAB!
scrivi un playbook che cicli in base a delle discriminanti

## Roles
La documentazione ufficiale definisce i ruoli come “Un modo di caricare automaticamente certi file di variabili, task e handlers, basandosi su una precisa struttura di dati”, facendo forza sulla possibilità di chiamare indirettamente da un singolo playbook, altri insiemi di playbook già definiti, con relativi file, dipendenze e contenuti correlati.

Se immaginiamo per esempio di dover aggiornare un applicativo web su più nodi contemporaneamente, oltre ovviamente a poter effettuare manualmente la procedure di deploy “come si è sempre fatto” oppure scrivere da zero il flusso di automazione per effettuarlo, possiamo prima cercare se esiste già un ruolo scritto che soddisfa i nostri requisiti.

Installando Ansible viene scaricato anche il tool ansible-galaxy, tramite il quale è possibile sia inizializzare le directory dei nuovi ruoli, sia cercare e scaricare ruoli ufficiali o forniti dalla community presenti sul repository pubblico. Nello snippet d’esempio seguente, cerchiamo ed installiamo un ruolo per installare Samba:
```
[ansible@cos1 roles]$ ansible-galaxy search samba | grep geerling
 geerlingguy.samba                        Samba for RHEL/CentOS.

[ansible@cos1 roles]$ ansible-galaxy install geerlingguy.samba
- downloading role 'samba', owned by geerlingguy
- downloading role from https://github.com/geerlingguy/ansible-role-samba/archive/1.1.3.tar.gz
- extracting geerlingguy.samba to /home/ansible/.ansible/roles/geerlingguy.samba
- geerlingguy.samba (1.1.3) was installed successfully
```

Con questo approccio possiamo evitare di riscrivere grosse porzioni di codice complicato per eseguire compiti semplici. Teniamo a mente che è comuque buona prassi rivedere sempre il codice prima di utilizzarlo all’interno dei nostri progetti in quanto l’approccio dell’utente che l’ ha creato potrebbe essere molto diverso da quello al quale siamo abituati.

Analizziamo un semplice playbook per comprendere il concetto chiave della chiamata ad un ruolo. Prendiamo come esempio questa brevissima sezione di codice relativa ad un main.yml che funge da entrypoint per il riutilizzo di cui sopra, il quale utilizza la sintassi “classica” attraverso la keyword roles:

```
---
- hosts: webservers
  vars: service=httpd
  roles:
    - ruolo_esempio
```

Questo snippet, per il ruolo_esempio designato:

Si limita a definire gli host sui quali eseguire i ruoli
Chiama indirettamente il file ./ruolo_esempio/tasks/main.yml
Definisce la variabile “service” che verrà passata al ruolo caricato
Così facendo si avvia anche l’esecuzione di ogni handler legato al ruolo, che sia definito nel playbook caricato tra i tasks, o comunque presente nella specifica sottodirectory del ruolo. Si include ogni variabile, si carica ogni eventuale dipendenza, si validano tutte le referenze legate a files, template e tasks.

Notiamo che la direttiva “service” definita a monte verrà ereditata così come ogni altra variabile, seguendo le regole di erediterietà e overriding classiche dello strumento Ansible.

Teniamo inoltre presente che, utilizzando il sistema dei ruoli, diviene ancor più utile un flow-control minuzioso… “pre_tasks” e “post_tasks”, al fine di orchestrare l’esecuzione nel suo insieme. Eseguendo compiti rispettivamente prima e dopo i ruoli richiamati.

La struttura della cartella nella quale è inserito il playbook è il primo posto in cui Ansible cercherà di risolvere i riferimenti a contenuti esterni. Per predisporre questa directory ci viene in aiuto il comando ansible-galaxy.

#ansible-galaxy init ruolo_esempio
Esplodiamo la directory corrente per spiegare nel dettaglio come richiamare del codice già definito:
```
ansible@cos1 roles]$ tree
├── main.yml
└── ruolo_esempio
    ├── defaults
    │   └── main.yml
    ├── files
    ├── handlers
    │   └── main.yml
    ├── meta
    │   └── main.yml
    ├── README.md
    ├── tasks
    │   └── main.yml
    ├── templates
    ├── tests
    │   ├── inventory
    │   └── test.yml
    └── vars
        └── main.yml
```
Possiamo notare che alla radice della cartella vi è un file main.yml, la cui sintassi chiama il file ./ruolo_esempio/tasks/main.yml attraverso il tag specifico “roles”. L’utilizzo di questo tag è il cuore del presente tutorial:
```
--- 
 hosts: thiscomputer
 become: true
 roles:
   - ruolo_esempio
Riporto il contenuto del file richiamato:

---
    - name: Playbook evocato dal primo main
      yum:
        name: "{{ service }}"
        state: present
```
Del quale osserviamo l’esecuzione attraverso il lancio del solo main.yml presente nella directory radice:
```
[ansible@cos1 roles]$ ansible-playbook main.yml
 
PLAY [thiscomputer] ******************************************************************************
TASK [Gathering Facts] ******************************************************************************
ok: [thiscomputer]
 
TASK [test2 : Playbook evocato dal primo main] ******************************************************************************
ok: [thiscomputer]
 
PLAY RECAP ******************************************************************************
thiscomputer: ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
```
Questo meccanismo, unito alla potenza del repository di ruoli ansible-galaxy, permette un forte riutilizzo del codice, venendoci in aiuto non solo nella definizione di automazione complesse, ma facendoci anche risparmiare molto tempo.

Valutiamo di contribuire al lavoro della community su Galaxy, così come noi possiamo beneficiare dello sforzo degli utenti, qualcuno potrebbe aver bisogno proprio del contenuti su cui stiamo lavorando.



## Bibliografia
ansible open source - https://docs.ansible.com/