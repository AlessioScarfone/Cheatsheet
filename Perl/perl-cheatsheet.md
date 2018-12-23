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

### Operatori e assegnazioni

```perl
+ 	#somma
- 	#sottrazione
* 	#moltiplicazione
/ 	#divisione
**	#potenza
%	#modulo

++$a; $a++ #pre e post incremento
--$a; $a-- #pre e post decremento

.	#concatenazione
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

#### Funzioni utili:

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

