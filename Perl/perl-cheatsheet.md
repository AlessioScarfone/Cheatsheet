# Perl 

Perl è un linguaggio di programmazione/scripting interpretato.

### Perl Basic Note

```bash
perl -v # verifica la versione di Perl

#Shabang
#!/usr/bin/perl

#esecuzione di uno script
perl script.pl
#oppure
chmod u+x script.pl
./script.pl

perl -w script.pl #mostra i warning più utili
perl -W script.pl #mostra TUTTI i warning
perl -d script.pl #avvia in modalità debugger

perl -e 'print 7**5' #run one line program 

#si possono includere per ricevere suggerimenti su possibli errori
use strict;
use warnings;

#PerlDoc
perldoc perlop #manuale degli operatori
perldoc -f [FUNC] #manuale per le funzioni

```

- Commenti:

```perl
# commento per singola riga

=begin comment
	...
	...
=cut
```

## Variabili

I nomi delle variabili sono precedute da un simbolo che ne definisce il tipo.

Tutti i nomi di variabili devono cominciare con una lettera o con un underscore.

```perl
$ 	#variabili scalari 
@	# array
%	# array associativi
&	#nomi delle funzioni (chiamate a funzioni)
```

**NOTA:**  le variabili definite con `my` sono definite come *"variabili  locali"*. Senza `my` viene creata una variabile globale.

In Perl le variabili `$_` e `@_` sono variabili globali di default

### Operatori e assegnazioni

```perl
+ 	#somma
- 	#sottrazione
* 	#moltiplicazione
/ 	#divisione
**	#potenza
%	#modulo

#varianti: (+=, -=, *=, /=, **=, %=)

++$a; $a++ #pre e post incremento
--$a; $a-- #pre e post decremento

.	#concatenazione

# OPERATORI DI COMPARAZIONE
### NUMERICI:
== , != , <, > , >= , <=
<=>	#Operatore di comparazione per ordinamento 

#STRINGHE:
### binding per espressioni regolari:
=~, !~
### COMPARAZIONE TRA STRINGHE:
eq		#eguaglianza
ne 		#ineguaglianza
gt,lt	#maggiore/minore di
ge,le 	#maggiore/minore o uguale
cmp		#Operatore di comparazione per ordinamento 

#OPERATORI LOGICI
&& , || , !, and , or, not ,xor

#OPERATORI BITWISE
#left shift (<<), right shift (>>),
#bitwise and (&), bitwise or (|) and bitwise xor (^),
#e le loro varianti con assegnamento (<<=, >>=, &=, |=, ^=)
```

Le doppie virgolette `""` forzano l'interpretazione del codice al loro interno, dunque verranno sostituiti i nomi delle variabili e i caratteri speciali (es. newline \n  e tab \t)

## Array

|           | AGGIUNGI  | RIMUOVI |
| :-------: | :-------: | :-----: |
| **CODA**  |  *push*   |  *pop*  |
| **TESTA** | *unshift* | *shift* |

```perl
@vuoto = (); 	#array vuoto
@cibo = ("mele","pere","uva");

@num = (1..4);		 #[1,2,3,4]
@let = ("a".."d");   #['a','b','c','d']

#accesso al singolo elemento
print $cibo[1]; #pere

push(@cibo,"pane");				#aggiungi in coda
push(@cibo,("latte","acqua"));

unshift(@cibo,"formaggio"); 	#aggiungi in testa

#split per spazio e riempe l'array
@altrocibo = qw/bistecca insalata/	

push(@cibo,@altrocibo);

$ultimo = pop(@cibo) 	#toglie in coda
$primo = shift(@cibo) 	#toglie in testa

#unione array
@merge = (@num,@let);

#DIMENSIONE DI UN ARRAY
$size = @array 		 #num di elementi
$lastindex = $#array #indice dell'ultimo elemento

# >> NOTA << stampa un array:
print @cibo  	#melaperauva
print "@cibo" 	#mela pera uva
print '@cibo'	#@cibo
```

- **ARRAY SLICE**

```perl
@a = (1..4);
print "@a \n";	#1 2 3 4
@b = @a[2,3];
print "@b"		#3 4
```

- **SPLICE**

```perl
#SPLICE: sostituisci o aggiungi elementi in un punto specifico dell'array
splice(@array,indexStart,numElemDaSostituire,listaNuoviElem);

@arr = (a..d);
@sostituiti = splice(@arr,1,1,("1","2"));
# [a 1 2 c d] sostituisce solo la "b" con 1 e aggiunge il 2
# $sostituiti = [b]

#se numElemDaSostituire=0 allora aggiunge solo senza sostituire
```

- **SPLIT**

```perl
$str = "ciao mondo !!";
@arr = split(/ /,$str);
($a , $b) =  split(/ /,$str); 	#$a = ciao , $b = mondo

print "@arr"
```

- **JOIN**

```perl
@lett = ("a".."f");
@joined = join("<>",@lett);	#a<>b<>c<>d<>e<>f

```


## File

```perl
$file = f.txt;
#APRI UN FILE
open(FILE,$file);
#Il primo è l' indicatore del file (handle) che viene usato in seguito per riferirsi al file.
#La funzione restituisce false  in caso di problemi e imposta la variabile $! che contiene il motivo del fallimento

if(!open(F,fileCheNonEsiste.txt)){
    die("File non aperto: $!");
}
#oppure
open(F,fileCheNonEsiste.txt) ||  die("File non aperto: $!");

#<HANDLE> legge il file
#il file viene letto tutto in una volta
@righe = <FILE>; 
#legge solo la prima riga
$r = <FILE> 

#scrivi su un file aperto in scrittura
print HANDLE "stringa";

#CHIUDI FILE
close(FILE);

```

| **APRI IN LETTURA**    | open(INFO,$file); <br />open(INFO,"<$file"); |
| ---------------------- | -------------------------------------------- |
| **APRI IN SCRITTURA**  | **open(NEW_F,">$file");**                    |
| **APRI PER APPENDERE** | **open(INFO,">>$file");**                    |

- **COPIARE UN FILE**

```perl
open(D1,"<file1.txt");
open(D2,">file2.txt");
while(<DATA>){
    print D2 $_;
}
close(D1);
close(D2);
```

- **RINOMINARE UN FILE**
```perl
  rename("/usr/test/file1.txt","/usr/test/file2.txt")
```


- **CANCELLARE UN FILE**
```perl
unlink("/usr/test/file1.txt");
```

- **APRIRE UNA DIRECTORY**
```perl
  opendir(DIR,"DirConFile");
  @files = readdir(DIR);
  
  #cerca file java
  @javaf = grep/.java$/,@files;
  
  closedir(DIR);
```

- **STDIN , STDOUT , STDERR**

3 filehandler aperti di default in ogni programma Perl.

**Come leggere da input:**

```perl
print "Inserisci qualcosa:";
$l =<STDIN>;

print "Input: $l \n";

#leggi tutte le righe inserite da input fino a ^D (ctrl+d)
@lines = <STDIN>
```



## Argomenti da linea di comando

```
for($i=0;$i<=$#ARGV;$i++){
    print "$ARGV[$i] ";
}
```



## Strutture di controllo

- **IF**

```perl
#postfix if
print $cont if ($cont > 10 && $cond < 50); 

#prefix if
if ($cont > 10){		
	print $cont;
} elsif ($cont > 5 ){
	print "ERROR 1"
} else {
    print "ERROR 2";
}

```

- **FOREACH & FOR**

```perl
@n=(1..10);
foreach my $i(@n){
    print "$i ";
}

for(my $i=0;$i<=$#n;$i++){
    print "$n[$i] ";
}

#quadrato dei primi 10 numeri
foreach (1 .. 10)
{
	print ’$_ * $_ = ’ . $_ * $_ . "\n";
}

for (@n)
{
	$_ **= 2;
}
```

- **WHILE & DO WHILE**

```perl
$i = <STDIN>;
while($i<3){
    print "OK, $i";
    
    $i = <STDIN>;
}


#salta il controllo al primo input
$i = <STDIN>;
do{
    print "OK, $i";
    
    $i = <STDIN>;
}while($i<3)

#loop infinito
for (;;) { ... }
while (1) { ... }

```

- **next**  = continue
- **last**  = break



## Invocazione comandi della shell

```perl
@list = qx(ls -l);
```

## Array Associativi

Associa coppie di stringhe (chiave, valore). 

```perl
%info = ('Michiele',39,'Mauro',19);
#oppure
%info_2 = (
	'Michiele'=> 39,
	'Mauro' => 19
);

print "Michele ha $info{'Michele'} anni";

#aggiungi o modifica un valore;
$info{'Alessio'} = 25;
#cancellare un valore
delete $info{'Alessio'};
#controlla se esiste una chiave
if(exists($info{'Alessio'})){
    #fai qualcosa
}
#conversione array associativo in array normale.
@infos = %info; #Michele 39 Ale 25 Mauro 19 

#KEYS: funzione che restituisce tutte le chiavi dell'array associativo
#VALUES: restituisce la lista di tutti i valori memorizzati nell'array
@chiavi = keys(%info);
@valori = values(%info);
#Le liste restituite hano lo stesso ordine, ma non ha nulla a che vedere
#con l'ordine di inserimento nell'array associativo

#in contesti scalari otteniamo i conteggi delle chiavi e dei valori
$num_chiavi = keys(%info);
$num_valori = values(%info);

#EACH: restituisce una coppia coppia di elementi dell'array
#esempio di stampa

while(($k,$v) = each(%info)){
    print "$k => $v \n";
}

foreach $k(keys(%info)){
    print "$k => $info{$k} \n";
}


```

**NOTA**: l'identificatore dell'elemento viene specificato tra **parentesi graffe** e non quadre.

## Subroutine

- Si definiscono tramite la keyword `sub`. 

- Per accedere agli argomenti passati alla funzione si usa l'array `@_`

```perl
sub pow_2{
    if(exists($_[0])){ 
    	return $_[0]**2;
    }else{
        print "ERROR";
    }
}

print pow_2(4)."\n";
```



## Espressioni Regolari

> Una espressione regolare (chiamata anche regex o regexp) è un pattern che descrive le caratteristiche di un particolare pezzo di testo.

Una espressione regolare è racchiusa tra 2 slash `/`



L'operatore di pattern matching è `=~`. Questo operatore verifica se esiste una corrispondenza tra una stringa ed una certa regex. L'operatore `!~` è utilizzato per rilevare la **non** corrispondenza.

Gli elementi principale di una espressione regolare sono:

- Elementi (Literals) : Rappresentano una parte di testo.
- Qauntificatori (Quantifiers): Indicano quante volte ci si aspetta che un certo elemento (o gruppo di elementi) possa essere ripetuto.



### Pattern matching

Un **pattern matching** si definisce tramite l'operazione di ricerca `m` (di solito sottinteso).

```perl
$t = "Ciao mondo!";
print "Ok" if $t=~/Ciao/;
```

**Modificatori di Regex**:

- /REGEX/`g` modificatore globale: ricerca ogni evenienza.
- /REGEX/`i` case-insensitive

> **Come avviene la verifica del match ?** Viene cercata la posizione più a sinistra in cui si  riscontra l’intera espressione regolare. La stringa viene esaminata da sinistra a destra finché non viene trovato un riscontro di regexp o finché il confronto fallisce.



#### CARATTERI SPECIALI

**METACARATTERI**

- **.**     Qualsiasi carattere escluso quello di una riga nuova
- **\\**     Annulla gli effetti del metacarattere successivo (escape)
- **^**    Identifica l’inizio di una riga; inoltre all’inizio di un gruppo nega il gruppo stesso
- **$**    Identifica la fine di una riga
- **|**    Indica una condizione OR
- **()**    Indicano un gruppo di caratteri
- **[]**    Indicano intervalli e classi di caratteri. Corrispondenza con uno qualsiasi dei caratteri contenuti. All'interno si può usare il simbolo `-` per definire intervalli di caratteri. Si può usare il carattere `^` se si vuole definire una negazione.

**QUANTIFICATORI**

- **\***      Indica 0 o tante occorrenze
- **+**      Indica 1 o tante occorrenze
- **?**      Indica al massimo 1 occorrenza
- **{n}**       Ricerca esattamente n occorrenze    
- **{n,}**      Ricerca minimo n occorrenze    
- **{n,m}**       Ricerca minimo n e massimo m occorrenze

**ALTRI METACARATTERI**

- **\t**     tab (HT, TAB)
- **\n**     newline (LF, NL)
- **\r**     return (CR)
- **\d**     Qualsiasi cifra = [0-9]
- **\D**     Qualsiasi carattere **non** cifra = \[^0-9]
- **\w**     Qualsiasi carattere alfanumerico [a-zA-Z0-9]
- **\W**     Qualsiasi carattere **non** alfanumerico \[^a-zA-Z0-9]
- **\s**     Qualsiasi carattere di spazio
- **\S**     Qualsiasi carattere che **non** è di tipo spazio

Spesso è necessario poter memorizzare dei pattern per cui c'è stato un match in modo da poterli riutilizzare. In Perl ogni stringa che soddisfa un match è memorizzata nelle variabili speciali `$1, .... ,$9`. Queste variabili funziona all'esterno del contesto di ricerca e memorizzano le sequenze effettivamente riscontrate nei raggruppamenti definiti dalle parentesi tonde `()`.

```perl
$stringa = "MNL TMS 74 M 02 L736 Y";
$stringa =~ /([A-Z]{3})\s([A-Z]{3})\s(\d{2})\s([A-Z])\s(\d{2})\s([A-Z][0-9]{3})\s([A-Z])/;
#stampa tutti i match
print "CF: $1;$2;$3;$4;$5;$6;$7\n";
```



### Sostituzioni

Perl permette di fare sostituzioni basate sulle corrispondenze individuate.
Il modo per fare questo è usare l’operatore `s`

```perl
$frase = "Ciao ciao Mondo!";
$frase =~ s/Ciao/HELLO/gi;
print "DOPO => $frase \n";  #DOPO => HELLO HELLO Mondo!   
```

Le variabili speciali $1, $2, etc. possono essere usate nelle espressioni regolari o nelle sostituzioni mediante i codici speciali `\1, ..., \9`.

```perl
#Racchiudere le lettere maiuscole tra i due punti ":"
$frase = "Ciao Mondo";
$frase =~ s/([A-Z])/:\1:/g;
print "DOPO => $frase \n";
```



### Trasformazioni

La funzione **tr** permette una traduzione (traslitterazione) carattere per carattere.

```perl
$frase = "Ciao Mondo";
$frase =~ tr/CM/HW/;
print "$frase"; #Hiao Wondo
```

