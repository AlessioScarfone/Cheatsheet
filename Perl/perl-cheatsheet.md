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



## STRUTTURE DI CONTROLLO

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

