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

### Variabili

I nomi delle variabili sono precedute da un simbolo che ne definisce il tipo.

Tutti i nomi di variabili devono cominciare con una lettera o con un underscore.

```perl
$ 	#variabili scalari 
@	# array
%	# array associativi
&	#nomi delle funzioni (chiamate a funzioni)
```

**NOTA:**  le variabili definite con `my` sono definite come *"variabili  locali"*. Senza `my` viene creata una variabile globale.

#### Operatori e assegnazioni

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



