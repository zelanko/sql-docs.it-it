---
title: ALTER TABLE - comando SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f656396455a8d5669debc158c3edc866491fcb5
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207010"
---
# <a name="alter-table---sql-command"></a>ALTER TABLE (comando SQL)
A livello di codice modifica la struttura di una tabella.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ALTER TABLE TableName1  
   ADD | ALTER [COLUMN] FieldName1  
      FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]  
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
 - Or -  
ALTER TABLE TableName1  
   ALTER [COLUMN] FieldName2  
      [NULL | NOT NULL]  
      [SET DEFAULT eExpression2]  
      [SET CHECK lExpression2 [ERROR cMessageText2]]  
      [DROP DEFAULT]  
      [DROP CHECK]  
 - Or -  
ALTER TABLE TableName1  
   [DROP [COLUMN] FieldName3]  
   [SET CHECK lExpression3 [ERROR cMessageText3]]  
   [DROP CHECK]  
   [ADD PRIMARY KEY eExpression3 TAG TagName2]  
   [DROP PRIMARY KEY]  
   [ADD UNIQUE eExpression4 [TAG TagName3]]  
   [DROP UNIQUE TAG TagName4]  
   [ADD FOREIGN KEY [eExpression5] TAG TagName4  
      REFERENCES TableName2 [TAG TagName5]]  
   [DROP FOREIGN KEY TAG TagName6 [SAVE]]  
   [RENAME COLUMN FieldName4 TO FieldName5]  
   [NOVALIDATE]  
```  
  
## <a name="arguments"></a>Argomenti  
 *TableName1*  
 Specifica il nome della tabella viene modificata la cui struttura.  
  
 Aggiungi [COLUMN] *FieldName1*  
 Specifica il nome del campo da aggiungere.  
  
 ALTER [COLUMN] *FieldName1*  
 Specifica il nome di un campo esistente da modificare.  
  
 *FieldType* [( *nFieldWidth* [, *nPrecision*]])  
 Specifica il tipo di campo, larghezza del campo e la precisione di campo (numero di posizioni decimali) per un campo nuovo o modificato.  
  
 *FieldType* è una singola lettera indicante che il campo [tipo di dati](../../odbc/microsoft/visual-foxpro-field-data-types.md). Alcuni tipi di dati del campo è necessario specificare *nFieldWidth* oppure *nPrecision* o entrambi.  
  
 *nFieldWidth* e *nPrecision* vengono ignorate per D, G, I, G, M, P, T e Y tipi. Per impostazione predefinita *nPrecision* non è zero (posizioni decimali) se *nPrecision* non viene incluso per i tipi di B, F e N.  
  
 NULL &#124; NOT NULL  
 Consente o impedisce che i valori null nel campo.  
  
 Se omette NULL e NOT NULL, l'impostazione corrente di SET NULL determina se sono consentiti valori null nel campo. Tuttavia, se si omette NULL e non NULL, include la clausola UNIQUE o PRIMARY KEY, viene ignorata l'impostazione corrente di SET NULL e il campo non è NULL per impostazione predefinita.  
  
 CONTROLLARE *lExpression1*  
 Specifica una regola di convalida per il campo. *lExpression1* deve restituire un'espressione logica e può essere una funzione definita dall'utente o una stored procedure. Ogni volta che viene aggiunto un record vuoto, viene verificata la regola di convalida. Viene generato un errore se la regola di convalida non supporta un valore di campo vuoto in un record accodato.  
  
 ERRORE *cMessageText1*  
 Specifica il messaggio di errore visualizzato quando la regola di convalida campo genera un errore.  
  
 DEFAULT *eExpression1*  
 Specifica un valore predefinito per il campo. Il tipo di dati *eExpression1* deve essere lo stesso come il tipo di dati per il campo.  
  
 PRIMARY KEY  
 Crea un tag di indice primario. Il tag di indice ha lo stesso nome del campo.  
  
 UNIQUE  
 Crea un tag di indice candidate con lo stesso nome del campo.  
  
> [!NOTE]  
>  Candidato gli indici (creati, includendo l'opzione univoco fornito per compatibilità con ANSI in ALTER TABLE o CREATE TABLE) sono diversi dagli indici creati tramite l'opzione univoco nel comando dell'indice. Le chiavi di indice duplicati; consente a un indice creato utilizzando UNIQUE nel comando indice gli indici candidato non consentono chiavi di indice duplicati.  
  
 I valori null e i record duplicati non sono consentiti in un campo che viene usato per un indice di primarie o candidate.  
  
 Se si sta creando un nuovo campo usando Aggiungi colonna, Visual FoxPro non genererà un errore se si crea un indice di primarie o candidate per un campo che supporta valori null. Tuttavia, Visual FoxPro genererà un errore se si tenta di immettere un valore null o duplicato in un campo che viene usato per un indice di primarie o candidate.  
  
 Se si modifica un campo esistente e il database primario o espressione di indice candidato è costituita da campi nella tabella, Visual FoxPro controlla i campi per vedere se contengono valori null o i record duplicati. In caso affermativo, Visual FoxPro genera un errore e la tabella non viene modificata.  
  
 I riferimenti *TableName2* TAG *TagName1*  
 Specifica la tabella padre alla quale viene stabilita una relazione permanente. TAG *TagName1* specifica i tag di indice della tabella padre in cui si basa la relazione. I nomi di tag di indice possono contenere fino a 10 caratteri.  
  
 NOCPTRANS  
 Impedisce la conversione a una tabella codici diversa per i campi di tipo carattere e memo. Se la tabella viene convertita in un'altra tabella codici, i campi per cui è stato specificato NOCPTRANS non vengono tradotti. NOCPTRANS può essere specificato solo per i campi di tipo carattere e memo.  
  
 L'esempio seguente crea una tabella denominata mytable contenente due campi di tipo carattere e i due campi di tipo memo. Il secondo campo a carattere char2 e il secondo campo di tipo memo, memo2, includere NOCPTRANS per impedire la traduzione.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLUMN] *FieldName2*  
 Specifica il nome di un campo esistente da modificare.  
  
 IMPOSTAZIONE del valore predefinito *eExpression2*  
 Specifica un nuovo valore predefinito per un campo esistente. Il tipo di dati *eExpression2* deve essere lo stesso come il tipo di dati per il campo.  
  
 CONTROLLO di SET *lExpression2*  
 Specifica una nuova regola di convalida per un campo esistente. *lExpression2* deve restituire un'espressione logica e può essere una funzione definita dall'utente o una stored procedure.  
  
 ERRORE *cMessageText2*  
 Specifica il messaggio di errore visualizzato quando la regola di convalida campo genera un errore. Il messaggio viene visualizzato solo quando i dati vengono modificati all'interno di una finestra di esplorazione o di modifica.  
  
 DROP DEFAULT  
 Rimuove il valore predefinito per un campo esistente.  
  
 CONTROLLO ELENCO  
 Rimuove la regola di convalida per un campo esistente.  
  
 Riepilogo [COLUMN] *FieldName3*  
 Specifica un campo da rimuovere dalla tabella. Rimozione di un campo dalla tabella rimuove anche regola di convalida campi e impostazione del valore del campo predefinito.  
  
 Se le espressioni chiave o un trigger di indice fa riferimento il campo, le espressioni diventano non valide quando il campo viene rimosso. In questo caso, un errore non viene generato quando il campo viene rimosso, ma le espressioni di chiave o un trigger di indice non valido verranno generati degli errori in fase di esecuzione.  
  
 CONTROLLO di SET *lExpression3*  
 Specifica la regola di convalida della tabella. *lExpression3* deve restituire un'espressione logica e può essere una funzione definita dall'utente o una stored procedure.  
  
 ERRORE *cMessageText3*  
 Specifica il messaggio di errore visualizzato quando la regola di convalida tabella genera un errore. Il messaggio viene visualizzato solo quando i dati vengono modificati all'interno di una finestra di esplorazione o di modifica.  
  
 CONTROLLO ELENCO  
 Rimuove la regola di convalida della tabella.  
  
 Aggiungi chiave primaria *eExpression3*TAG *TagName2*  
 Aggiunge un indice primario per la tabella. *eExpression3* specifica l'espressione chiave di indice primario, e *TagName2* specifica il nome del tag indice primario. I nomi di tag di indice possono contenere fino a 10 caratteri. Se TAG *TagName2* viene omesso e *eExpression3* è un singolo campo, il tag di indice primario ha lo stesso nome del campo specificato in *eExpression3*.  
  
 ELIMINA CHIAVE PRIMARIA  
 Rimuove l'indice primario e il tag di indice. Poiché una tabella può avere solo una chiave primaria, non è necessario specificare il nome della chiave primaria. Rimozione dell'indice primario vengono eliminate anche le eventuali relazioni persistenti in base alla chiave primaria.  
  
 Aggiungi UNIQUE *eExpression4*[TAG *TagName3*]  
 Aggiunge un indice di candidati per la tabella. *eExpression4* specifica l'espressione della chiave indice candidato, e *TagName3* specifica il nome del tag indice candidato. I nomi di tag di indice possono contenere fino a 10 caratteri. Se si omette TAG *TagName3* e, se *eExpression4* è un singolo campo, il tag di indice candidato ha lo stesso nome del campo specificato in *eExpression4*.  
  
 ELENCO di TAG univoco *TagName4*  
 Rimuove l'indice candidato e privo di tag di indice. Poiché una tabella può avere più chiavi candidate, è necessario specificare il nome del tag indice candidato.  
  
 ADD FOREIGN KEY [ *eExpression5*] TAG *TagName4*  
 Aggiunge un indice (non primaria) esterno alla tabella. *eExpression5* specifica l'espressione della chiave esterna dell'indice, e *TagName4* specifica il nome del tag indice esterna. I nomi di tag di indice possono contenere fino a 10 caratteri.  
  
 I riferimenti *TableName2*[TAG *TagName5*]  
 Specifica la tabella padre alla quale viene stabilita una relazione permanente. Includere TAG *TagName5* per stabilire una relazione basata su un tag di indice esistente per la tabella padre. I nomi di tag di indice possono contenere fino a 10 caratteri. Se si omette TAG *TagName5*, la relazione viene stabilita tramite tag di indice primario della tabella padre.  
  
 TAG di chiave esterna di rilascio *TagName6*[salvare]  
 Elimina una chiave esterna con il tag dell'indice viene *TagName6*. Se si omette il salvataggio, il tag di indice viene eliminato dall'indice struttura. Includere salvare per impedire l'eliminazione del tag dell'indice dall'indice struttura.  
  
 COLONNA di RIDENOMINAZIONE *FieldName4*TO *FieldName5*  
 Consente di modificare il nome di un campo nella tabella. *FieldName4* specifica il nome del campo in cui è stato rinominato. *FieldName5* specifica il nuovo nome del campo.  
  
> [!CAUTION]  
>  Prestare attenzione durante la ridenominazione di campi della tabella, perché le espressioni di indice, le regole di convalida campi e tabelle, i comandi e funzioni possono fare riferimento a nomi di campo originale.  
  
 NOVALIDATE  
 Specifica che Visual FoxPro consente modifiche da apportare alla struttura della tabella. Queste modifiche potrebbero violare l'integrità dei dati nella tabella. Per impostazione predefinita, Visual FoxPro impedisce ALTER TABLE di apportare modifiche che violano l'integrità dei dati nella tabella. Includere NOVALIDATE per eseguire l'override di questo comportamento predefinito.  
  
## <a name="remarks"></a>Note  
 È possibile utilizzare ALTER TABLE per modificare la struttura di una tabella che non è stato aggiunto a un database. Tuttavia, Visual FoxPro genera un errore se si includono l'impostazione predefinita, FOREIGN KEY, PRIMARY KEY, riferimenti, o quando si modifica una tabella gratuita di clausole SET.  
  
 ALTER TABLE può ricompilare la tabella creando una nuova intestazione di tabella e Accodamento di record per l'intestazione della tabella. Ad esempio, la modifica di tipo o la larghezza del campo potrebbe causare la tabella da ricompilare.  
  
 Dopo che una tabella viene ricompilata, vengono eseguite le regole di convalida campi per tutti i campi il cui tipo o la cui larghezza viene modificati. Se si modifica il tipo o la larghezza di un campo nella tabella, viene eseguita la regola della tabella.  
  
 Se si modificano le regole di convalida campo o una tabella per una tabella che dispone di record, Visual FoxPro testa le nuove regole di convalida campo o una tabella in base a quelli esistenti e genera un avviso alla prima occorrenza di una regola di convalida campo o una tabella o di una violazione di trigger.  
  
 Se la tabella che è modificare in un database, ALTER TABLE - SQL richiede l'uso esclusivo del database. Per aprire un database per l'utilizzo esclusivo, includere esclusivo nel DATABASE di aprire.  
  
## <a name="see-also"></a>Vedere anche  
 [Crea tabella - comando SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INDEX (comando)](../../odbc/microsoft/index-command.md)
