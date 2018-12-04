---
title: Connessione a bcp | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bcp
ms.assetid: 3eca5717-e50f-40db-be16-a1cebbdfee70
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 903106b5dfc17b98aae0614bd7b168d9b3acdf11
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527529"
---
# <a name="connecting-with-bcp"></a>Connessione a bcp
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

L'utilità [bcp](https://go.microsoft.com/fwlink/?LinkID=190626) è disponibile in [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Linux e macOS. Questa pagina illustra le differenze rispetto alla versione di Windows di `bcp`.
  
- Il carattere di terminazione del campo è tabulazione ("\t").  
  
- Il carattere di terminazione della riga è nuova riga ("\n").  
  
- La modalità carattere è il formato preferito per i file di formato `bcp` e i file di dati che non contengono caratteri estesi.  
  
> [!NOTE]  
> Una barra rovesciata '\\' in un argomento della riga di comando deve essere racchiusa tra virgolette o preceduta da un carattere di escape. Per specificare un carattere di nuova riga come carattere di terminazione della riga personalizzato, ad esempio, è necessario usare uno dei meccanismi seguenti:  
>   
> -   -r\\\n  
> -   -r "\n"  
> -   -r '\n'  
  
Di seguito è riportato un esempio di chiamata a un comando `bcp` per copiare le righe di una tabella in un file di testo:  
  
```  
bcp AdventureWorks2008R2.Person.Address out test.dat -Usa -Pxxxx -Sxxx.xxx.xxx.xxx  
```  
  
## <a name="available-options"></a>Opzioni disponibili
Nella versione corrente sono disponibili le opzioni e la sintassi seguenti:  

[_database_**.**] _schema_**.** _tabella_ **nelle** _data\_file_ | **out** _dati\_file_

- -a *packet_size*  
Specifica il numero di byte inviati al e dal server per ogni pacchetto di rete.  
  
- -b *batch_size*  
Specifica il numero di righe per ogni batch di dati importati.  
  
- -c  
Usa dati di tipo carattere.  
  
- -d *database_name*  
Specifica il database al quale connettersi.  
  
- -d  
Indica che il valore passato all'opzione -S di `bcp` deve essere interpretato come nome dell'origine dati (DSN). Per altre informazioni, vedere "Supporto di DSN in sqlcmd e bcp" in [Connessione con sqlcmd](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md).  
  
- -e *file_errori*Specifica il percorso completo di un file di errori usato per archiviare le eventuali righe che l'utilità `bcp` non è in grado di trasferire dal file al database.  
  
- -E  
Usa i valori Identity per la colonna Identity nel file di dati importato.  
  
- -f *format_file*  
Specifica il percorso completo di un file di formato.  
  
- -F *first_row*  
Specifica il numero della prima riga da esportare da una tabella o da importare da un file di dati.  
  
- -k  
Specifica che durante l'operazione il valore delle colonne vuote deve essere Null, ovvero che non verranno inseriti valori predefiniti in tali colonne.  
  
- -l  
Specifica un timeout accesso. L'opzione -l specifica il numero di secondi che devono trascorrere prima che si verifichi il timeout di un accesso a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando si prova la connessione a un server. Il timeout di accesso predefinito è 15 secondi. Il valore del timeout deve essere un numero compreso tra 0 e 65534. Se il valore specificato non è numerico o non è compreso in tale intervallo, `bcp` genera un messaggio di errore. Un valore pari a 0 specifica un timeout infinito.
  
- -L *last_row*  
Specifica il numero dell'ultima riga da esportare da una tabella o da importare da un file di dati.  
  
- -m *max_errors*  
Specifica il numero massimo di errori di sintassi che possono verificarsi prima dell'annullamento dell'operazione di `bcp`.  
  
- -n  
Esegue l'operazione di copia bulk usando i tipi di dati nativi del database.  
  
- -P *password*  
Specifica la password per l'ID di accesso.  
  
- -Q  
Esegue l'istruzione SET QUOTED_IDENTIFIERS ON durante la connessione tra l'utilità `bcp` e l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
- -r *row_terminator*  
Specifica il carattere di terminazione della riga.  
  
- -r  
Specifica che la copia bulk dei dati relativi a valuta, data e ora verrà eseguita in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando il formato definito per le impostazioni locali del computer client.  
  
- -S *server*  
Specifica il nome del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] istanza a cui connettersi, o se -D viene usata, un DSN.  
  
- -t *field_terminator*  
Specifica il carattere di terminazione del campo.  
  
- -T  
Specifica che l'utilità `bcp` si connette a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tramite una connessione trusted che usa la sicurezza integrata.  
  
- -U *login_id*  
Specifica l'ID di accesso utilizzato per connettersi a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
- -V  
Visualizza numero di versione e informazioni sul copyright per l'utilità `bcp`.  
  
- -w  
Esegue l'operazione di copia bulk usando caratteri Unicode.  
  
In questa versione sono supportati i caratteri Latin 1 e UTF-16.  
  
## <a name="unavailable-options"></a>Opzioni non disponibili
Nella versione corrente non sono disponibili le opzioni e la sintassi seguenti:  

- -c  
Specifica la tabella codici dei dati contenuti nel file di dati.  
  
- -h *hint*  
Specifica gli hint usati per l'importazione bulk di dati in una tabella o in una vista.  
  
- -i *input_file*  
Specifica il nome di un file di risposta.  
  
- -n  
Usa i tipi di dati nativi del database per i dati non di tipo carattere e i caratteri Unicode per i dati di tipo carattere.  
  
- -o *output_file*  
Specifica il nome di un file in cui viene reindirizzato l'output dal prompt dei comandi.  
  
- -V (80 | 90 | 100)  
Vengono usati tipi di dati da una versione precedente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
- -X  
Se usato con le opzioni format e -f format_file, genera un file di formato basato su XML anziché un file di formato predefinito non XML.  
  
## <a name="see-also"></a>Vedere anche

[Connessione a **sqlcmd**](../../../connect/odbc/linux-mac/connecting-with-sqlcmd.md)  
