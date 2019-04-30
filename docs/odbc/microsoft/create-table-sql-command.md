---
title: Crea tabella - comando SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE [ODBC]
ms.assetid: be2143ba-fc16-42c9-84f7-8985cd924860
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 62d13bdc9d1a0fc030dc33bf982f6561b454c4ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232288"
---
# <a name="create-table---sql-command"></a>CREATE TABLE (comando SQL)
Crea una tabella con i campi specificati.  
  
 Il Driver ODBC Visual FoxPro supporta la sintassi del linguaggio Visual FoxPro nativa per questo comando. Per informazioni specifiche del driver, vedere **osservazioni Driver**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CREATE TABLE | DBF TableName1 [NAME LongTableName] [FREE]  
   (FieldName1FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]   
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
   [, FieldName2 ...]  
      [, PRIMARY KEY eExpression2 TAG TagName2  
      |, UNIQUE eExpression3 TAG TagName3]  
      [, FOREIGN KEY eExpression4 TAG TagName4 [NODUP]  
            REFERENCES TableName3 [TAG TagName5]]  
      [, CHECK lExpression2 [ERROR cMessageText2]])  
| FROM ARRAY ArrayName  
```  
  
## <a name="arguments"></a>Argomenti  
 CREATE TABLE &#124; DBF *TableName1*  
 Specifica il nome della tabella da creare. Le opzioni di tabella e DBF sono identiche.  
  
 NOME *LongTableName*  
 Specifica un nome per la tabella lungo. Solo quando un database è aperto, poiché i nomi di tabella lunghi vengono archiviati nei database, è possibile specificare un nome di tabella lunghi.  
  
 I nomi lunghi possono contenere fino a 128 caratteri e possono essere utilizzati al posto di nomi file brevi nel database.  
  
 FREE  
 Specifica che la tabella non verrà aggiunto a un database aperto. GRATUITO non è necessaria se un database non è aperto.  
  
 *(FieldName1 FieldType* [( *nFieldWidth* [, *nPrecision*])]  
 Specifica il nome del campo, tipo di campo, larghezza del campo e la precisione di campo (numero di posizioni decimali), rispettivamente.  
  
 *FieldType* è una singola lettera indicante il campo [tipo di dati](../../odbc/microsoft/visual-foxpro-field-data-types.md). Alcuni tipi di dati del campo è necessario specificare *nFieldWidth* oppure *nPrecision* o entrambi.  
  
 *nFieldWidth* e *nPrecision* vengono ignorate per D, G, I, G, M, P, T e Y tipi. *nPrecision* valore predefinito è zero (senza posizioni decimali) se *nPrecision* non è incluso per i tipi di B, F e N.  
  
 NULL  
 Ammette valori null nel campo.  
  
 NOT NULL  
 Impedisce che i valori null nel campo.  
  
 Se omette NULL e NOT NULL, l'impostazione corrente di SET NULL determina se sono consentiti valori null nel campo. Tuttavia, se si omette NULL e non NULL, include la clausola UNIQUE o PRIMARY KEY, viene ignorata l'impostazione corrente di SET NULL e il campo valore predefinito è NOT NULL.  
  
 CHECK *lExpression1*  
 Specifica una regola di convalida per il campo. *lExpression1* può essere una funzione definita dall'utente. Ogni volta che viene aggiunto un record vuoto, viene verificata la regola di convalida. Viene generato un errore se la regola di convalida non consente un valore di campo vuoto in un record accodato.  
  
 ERROR *cMessageText1*  
 Specifica il messaggio di errore di Visual FoxPro viene visualizzato quando la regola di campo genera un errore. Il messaggio viene visualizzato solo quando si modificano i dati all'interno di una finestra di ricerca o una finestra di modifica.  
  
 DEFAULT *eExpression1*  
 Specifica un valore predefinito per il campo. Il tipo di dati *eExpression1* deve essere uguale al tipo di dati del campo.  
  
 PRIMARY KEY  
 Crea un indice primario per il campo. Il tag di indice primario ha lo stesso nome del campo.  
  
 UNIQUE  
 Crea un indice di candidati per il campo. Il tag di indice candidato ha lo stesso nome del campo.  
  
> [!NOTE]  
>  Candidato gli indici (creati, includendo l'opzione univoco nell'istruzione CREATE TABLE o ALTER TABLE - SQL) non sono uguali come gli indici creati con l'opzione nel comando indice univoco. Le chiavi di indice duplicati; consente a un indice creato con l'opzione nel comando indice univoco gli indici candidato non consentono chiavi di indice duplicati. Visualizzare [indice](../../odbc/microsoft/index-command.md) per ulteriori informazioni sulla relativa opzione univoco.  
  
 I valori null e i record duplicati non consentiti in un campo usato per un indice di primarie o candidate. Tuttavia, Visual FoxPro non genererà un errore se si crea un indice di primarie o candidate per un campo che supporta valori null. Se si tenta di immettere un valore null o duplicato in un campo usato per un indice di primarie o candidate, Visual FoxPro genererà un errore.  
  
 REFERENCES *TableName2*[TAG *TagName1*]  
 Specifica la tabella padre alla quale viene stabilita una relazione permanente. Se si omette TAG *TagName1*, la relazione viene stabilita usando la chiave di indice primario della tabella padre. Se la tabella padre non dispone di un indice primario, Visual FoxPro genera un errore.  
  
 Includere TAG *TagName1* per stabilire una relazione basata su un tag di indice esistente per la tabella padre. I nomi di tag di indice possono contenere fino a 10 caratteri.  
  
 La tabella padre non può essere una tabella gratuita.  
  
 NOCPTRANS  
 Impedisce la conversione a una tabella codici diversa per i campi di tipo carattere e memo. Se la tabella viene convertita in un'altra tabella codici, i campi per cui è stato specificato NOCPTRANS non vengono tradotti. NOCPTRANS può essere specificato solo per i campi di tipo carattere e memo.  
  
 L'esempio seguente crea una tabella denominata mytable contenente due campi di tipo carattere e i due campi di tipo memo. Il secondo campo a carattere char2 e il secondo campo di tipo memo, memo2, includere NOCPTRANS per impedire la traduzione.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 PRIMARY KEY *eExpression2* TAG *TagName2*  
 Specifica un indice primario per creare. *eExpression2* specifica qualsiasi campo o una combinazione dei campi nella tabella. TAG *TagName2* specifica il nome del tag di indice primario che viene creato. I nomi di tag di indice possono contenere fino a 10 caratteri.  
  
 Poiché una tabella può avere un solo indice primario, è possibile includere questa clausola se è già stato creato un indice primario per un campo. Se si include più di una clausola di chiave primaria nell'istruzione CREATE TABLE, Visual FoxPro genera un errore.  
  
 UNIQUE *eExpression3*TAG *TagName3*  
 Crea un indice di candidati. *eExpression3* specifica qualsiasi campo o una combinazione dei campi nella tabella. Tuttavia, se è stato creato un indice primario con una delle opzioni chiave primaria, è possibile includere il campo specificato per l'indice primario. TAG *TagName3* specifica un nome di tag per il tag di indice candidato che viene creato. I nomi di tag di indice possono contenere fino a 10 caratteri.  
  
 Una tabella può avere più indici candidato.  
  
 CHIAVE esterna *eExpression4*TAG *TagName4*[NODUP]  
 Crea un indice (non primaria) esterno e stabilisce una relazione a una tabella padre. *eExpression4* specifica l'espressione della chiave esterna dell'indice, e *TagName4* specifica il nome del tag chiave esterna indice creato *.* I nomi di tag di indice possono contenere fino a 10 caratteri. Includere NODUP per creare un indice esterna candidato.  
  
 È possibile creare più indici esterni per la tabella, ma le espressioni di indice esterna devono specificare diversi campi nella tabella.  
  
 REFERENCES *TableName3*[TAG *TagName5*]  
 Specifica la tabella padre alla quale viene stabilita una relazione permanente. Includere TAG *TagName5* per stabilire una relazione basata su un tag di indice per la tabella padre. I nomi di tag di indice possono contenere fino a 10 caratteri. Per impostazione predefinita, se si omette TAG *TagName5,* la relazione viene stabilita tramite chiave di indice primario della tabella padre.  
  
 CHECK *eExpression2*[ERROR *cMessageText2*]  
 Specifica la regola di convalida della tabella. ERRORE *cMessageText2* specifica il messaggio di errore di Visual FoxPro viene visualizzato quando viene eseguita la regola di convalida della tabella. Il messaggio viene visualizzato solo quando i dati viene modificati all'interno di una finestra Sfoglia o finestra Modifica.  
  
 DALLA matrice *ArrayName*  
 Specifica il nome di una matrice esistente il cui contenuto è il nome, tipo, precisione e scala per ogni campo nella tabella. Il contenuto della matrice può essere definito con la **AFIELDS**funzione ().  
  
## <a name="remarks"></a>Note  
 La nuova tabella viene aperto nell'area più basso disponibile lavoro ed è possibile accedervi mediante il relativo alias. La nuova tabella viene aperto in modalità esclusiva, indipendentemente dall'impostazione corrente di SET esclusivo.  
  
 Se un database è aperto e non si include la clausola gratuita, la nuova tabella viene aggiunta al database. È possibile creare una nuova tabella con lo stesso nome di una tabella nel database.  
  
 Se un database è aperto, CREATE TABLE - SQL richiede l'uso esclusivo del database. Per aprire un database per l'utilizzo esclusivo, includere esclusivo nel DATABASE di aprire.  
  
 Se non è un database aperto quando si crea la nuova tabella, tra cui le clausole di nome, CHECK, DEFAULT, FOREIGN KEY, PRIMARY KEY o riferimenti genera un errore.  
  
> [!NOTE]  
>  Sintassi di CREATE TABLE Usa le virgole per separare alcune opzioni di CREATE TABLE. Inoltre, il NULL, non NULL, controllo, predefinito, chiave primaria e univoco clausola deve trovarsi all'interno delle parentesi che contiene le definizioni di colonna.  
  
## <a name="driver-remarks"></a>Sezione Osservazioni di driver  
 Quando l'applicazione invia l'istruzione ODBC SQL CREATE TABLE all'origine dati, il Driver ODBC Visual FoxPro traduce il comando al comando Visual FoxProCREATE tabella utilizzando la sintassi illustrata nella tabella seguente.  
  
|Sintassi ODBC|Sintassi di Visual FoxPro|  
|-----------------|--------------------------|  
|CREATE TABLE *nome-tabella di base*<br /><br /> (*identificatore di colonna tipo di dati*<br /><br /> [NOT NULL]<br /><br /> [,*-identificatore della colonna tipo di dati*<br /><br /> [NOT NULL] ...)|Crea tabella *TableName1* [nome *LongTableName*]<br /><br /> (*FieldName1* *FieldType*<br /><br /> [(*nFieldWidth* [, *nPrecision*])]<br /><br /> [NOT NULL])|  
  
 Quando si crea una tabella usando il driver, il driver nella tabella si chiude immediatamente dopo la creazione di consentire l'accesso alla tabella da altri utenti. Questo comportamento è diverso da Visual FoxPro, che rimane aperto in modo esclusivo al momento della creazione della tabella. Tuttavia, se viene eseguita una stored procedure nell'origine dati che contiene un'istruzione CREATE TABLE, la tabella viene lasciata aperta.  
  
 Se l'origine dati è un database (file DBC), il Driver ODBC Visual FoxPro crea una tabella denominata *LongTableName* con lo stesso nome il *nome-tabella di base*.  
  
### <a name="using-data-definition-language-ddl"></a>Usando Data Definition Language (DDL)  
 Non è possibile includere DDL nelle posizioni seguenti:  
  
-   In un'istruzione SQL del batch che richiede una transazione  
  
-   In modalità di commit manuale, dopo un'istruzione che richiedevano una transazione, a meno che l'applicazione chiama innanzitutto **SQLTransact**.  
  
 Ad esempio, se si desidera creare una tabella temporanea, si deve creare la tabella prima di iniziare l'istruzione che richiedono una transazione. Se si include l'istruzione CREATE TABLE in un batch istruzione SQL che richiede una transazione, il driver restituisce un messaggio di errore.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER TABLE - comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Tipi di dati supportati (Driver ODBC Visual FoxPro)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [INSERT - comando SQL](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT (comando SQL)](../../odbc/microsoft/select-sql-command.md)
