---
title: CREATE TABLE - Comando SQL Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dfc80a56a021b1bfeda38115e79f7086632900c8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298691"
---
# <a name="create-table---sql-command"></a>CREATE TABLE (comando SQL)
Crea una tabella con i campi specificati.  
  
 Il driver ODBC di Visual FoxPro supporta la sintassi nativa del linguaggio Visual FoxPro per questo comando. Per informazioni specifiche del driver, vedere **Osservazioni del driver**.  
  
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
 CREATE TABLE &#124; *NomeTabella DBF1*  
 Specifica il nome della tabella da creare. Le opzioni TABLE e DBF sono identiche.  
  
 NOME *LongTableName*  
 Specifica un nome lungo per la tabella. Un nome di tabella lungo può essere specificato solo quando un database è aperto, perché i nomi di tabella lunghi vengono archiviati nei database.  
  
 I nomi lunghi possono contenere fino a 128 caratteri e possono essere utilizzati al posto dei nomi di file brevi nel database.  
  
 FREE  
 Specifica che la tabella non verrà aggiunta a un database aperto. Non è necessario GRATUITAMENTE se un database non è aperto.  
  
 *(NomeCampo1 TipoCampo* [( *nLarghezzaCampo* [, *nPrecision*])]  
 Specifica rispettivamente il nome del campo, il tipo di campo, la larghezza e la precisione del campo (numero di posizioni decimali).  
  
 *FieldType* è una singola lettera che indica il [tipo di dati](../../odbc/microsoft/visual-foxpro-field-data-types.md)del campo. Alcuni tipi di dati di campo richiedono l'immissione di *nFieldWidth* o *nPrecision* o entrambi.  
  
 *nFieldWidth* e *nPrecision* vengono ignorati per i tipi D, G, I, L, M, P, T e Y. *nPrecision* per impostazione predefinita è zero (senza cifre decimali) se *nPrecision* non è incluso per i tipi B, F o N.  
  
 NULL  
 Consente valori Null nel campo.  
  
 NOT NULL  
 Impedisce valori Null nel campo.  
  
 Se si omette NULL e NOT NULL, l'impostazione corrente di SET NULL determina se i valori Null sono consentiti nel campo. Tuttavia, se si omette NULL e NOT NULL e si include la clausola PRIMARY KEY o UNIQUE, l'impostazione corrente di SET NULL viene ignorata e il valore predefinito del campo è NOT NULL.  
  
 CHECK *lExpression1*  
 Specifica una regola di convalida per il campo. *lExpression1* può essere una funzione definita dall'utente. Ogni volta che viene aggiunto un record vuoto, viene controllata la regola di convalida. Se la regola di convalida non consente un valore di campo vuoto in un record accodato, viene generato un errore.  
  
 ERRORE *cMessageText1*  
 Specifica il messaggio di errore Viene visualizzato Visual FoxPro quando la regola di campo genera un errore. Il messaggio viene visualizzato solo quando i dati vengono modificati all'interno di una finestra Sfoglia o di una finestra Modifica.  
  
 DEFAULT *eExpression1*  
 Specifica un valore predefinito per il campo. Il tipo di dati di *eExpression1* deve essere lo stesso del tipo di dati del campo.  
  
 PRIMARY KEY  
 Crea un indice primario per il campo. Il tag di indice primario ha lo stesso nome del campo.  
  
 UNIQUE  
 Crea un indice candidato per il campo. Il tag di indice candidato ha lo stesso nome del campo.  
  
> [!NOTE]  
>  Gli indici candidati (creati includendo l'opzione UNIQUE in CREATE TABLE o ALTER TABLE - SQL) non sono gli stessi degli indici creati con l'opzione UNIQUE nel comando INDEX. Un indice creato con l'opzione UNIQUE nel comando INDEX consente chiavi di indice duplicate; gli indici candidati non consentono chiavi di indice duplicate. Vedere [INDICE](../../odbc/microsoft/index-command.md) per ulteriori informazioni sull'opzione UNIQUE.  
  
 I valori Null e i record duplicati non sono consentiti in un campo utilizzato per un indice primario o candidato. Tuttavia, Visual FoxPro non genererà un errore se si crea un indice primario o candidato per un campo che supporta valori null. Visual FoxPro genererà un errore se si tenta di immettere un valore null o duplicato in un campo utilizzato per un indice primario o candidato.  
  
 REFERENCES *NomeTabella2*[Tag *TagName1*]  
 Specifica la tabella padre in cui viene stabilita una relazione permanente. Se si osporà TAG *TagName1*, la relazione viene stabilita utilizzando la chiave di indice primaria della tabella padre. Se la tabella padre non dispone di un indice primario, Visual FoxPro genera un errore.  
  
 Includere TAG *TagName1* per stabilire una relazione basata su un tag di indice esistente per la tabella padre. I nomi dei tag di indice possono contenere fino a 10 caratteri.  
  
 La tabella padre non può essere una tabella libera.  
  
 NOCPTRANS  
 Impedisce la conversione in una tabella codici diversa per i campi carattere e memo. Se la tabella viene convertita in un'altra tabella codici, i campi per i quali è stato specificato NOCPTRANS non vengono convertiti. NOCPTRANS può essere specificato solo per i campi carattere e memo.  
  
 Nell'esempio seguente viene creata una tabella denominata mytable contenente due campi carattere e due campi memo. Il secondo campo carattere, char2, e il secondo campo memo, memo2, includono NOCPTRANS per impedire la conversione.  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 PRIMARY KEY *eExpression2* TAG *TagName2*  
 Specifica un indice primario da creare. *eExpression2* specifica qualsiasi campo o combinazione di campi nella tabella. TAG *TagName2* specifica il nome per il tag di indice primario che viene creato. I nomi dei tag di indice possono contenere fino a 10 caratteri.  
  
 Poiché una tabella può avere un solo indice primario, non è possibile includere questa clausola se è già stato creato un indice primario per un campo. Visual FoxPro genera un errore se si include più di una clausola PRIMARY KEY in CREATE TABLE.  
  
 UNIQUE *eExpression3*TAG *TagName3*  
 Crea un indice candidato. *eExpression3* specifica qualsiasi campo o combinazione di campi nella tabella. Tuttavia, se è stato creato un indice primario con una delle opzioni PRIMARY KEY, non è possibile includere il campo specificato per l'indice primario. TAG *TagName3* specifica un nome di tag per il tag di indice candidato che viene creato. I nomi dei tag di indice possono contenere fino a 10 caratteri.  
  
 Una tabella può avere più indici candidati.  
  
 FOREIGN KEY *eExpression4*TAG *TagName4*[NODUP]  
 Crea un indice esterno (non primario) e stabilisce una relazione con una tabella padre. *eExpression4* specifica l'espressione di chiave di indice esterna e *TagName4* specifica il nome del tag di chiave di indice esterna creato. I nomi dei tag di indice possono contenere fino a 10 caratteri. Includere NODUP per creare un indice esterno candidato.  
  
 È possibile creare più indici esteri per la tabella, ma le espressioni di indice esterno devono specificare campi diversi nella tabella.  
  
 REFERENCES *NomeTabella3*[Tag *TagName5*]  
 Specifica la tabella padre in cui viene stabilita una relazione permanente. Includere TAG *TagName5* per stabilire una relazione basata su un tag di indice per la tabella padre. I nomi dei tag di indice possono contenere fino a 10 caratteri. Per impostazione predefinita, se si omettendo TAG *TagName5,* la relazione viene stabilita utilizzando la chiave di indice primaria della tabella padre.  
  
 CHECK *eExpression2*[ERRORE *cMessageText2*]  
 Specifica la regola di convalida della tabella. Errore *cMessageText2* specifica il messaggio di errore visualizzato da Visual FoxPro quando viene eseguita la regola di convalida della tabella. Il messaggio viene visualizzato solo quando i dati vengono modificati all'interno di una finestra Sfoglia o Modifica.  
  
 FROM ARRAY *ArrayName*  
 Specifica il nome di una matrice esistente il cui contenuto è il nome, il tipo, la precisione e la scala per ogni campo della tabella. Il contenuto della matrice può essere definito con la funzione **AFIELDS**( ).  
  
## <a name="remarks"></a>Osservazioni  
 La nuova tabella viene aperta nell'area di lavoro più bassa disponibile ed è accessibile dal relativo alias. La nuova tabella viene aperta in modo esclusivo, indipendentemente dall'impostazione corrente di SET EXCLUSIVE.  
  
 Se un database è aperto e non si include la clausola FREE, la nuova tabella viene aggiunta al database. Non è possibile creare una nuova tabella con lo stesso nome di una tabella nel database.  
  
 Se un database è aperto, CREATE TABLE - SQL richiede l'utilizzo esclusivo del database. Per aprire un database per l'utilizzo esclusivo, includere EXCLUSIVE in OPEN DATABASE.  
  
 Se un database non è aperto quando si crea la nuova tabella, incluse le clausole NAME, CHECK, DEFAULT, FOREIGN KEY, PRIMARY KEY o REFERENCES genera un errore.  
  
> [!NOTE]  
>  La sintassi CREATE TABLE utilizza virgole per separare alcune opzioni CREATE TABLE. Inoltre, la clausola NULL, NOT NULL, CHECK, DEFAULT, PRIMARY KEY e UNIQUE deve essere inserita tra parentesi contenenti le definizioni di colonna.  
  
## <a name="driver-remarks"></a>Osservazioni del conducente  
 Quando l'applicazione invia l'istruzione SQL ODBC CREATE TABLE all'origine dati, il driver ODBC di Visual FoxPro converte il comando nel comando di Visual FoxProCREATE TABLE utilizzando la sintassi illustrata nella tabella seguente.  
  
|Sintassi ODBC|Sintassi di Visual FoxPro|  
|-----------------|--------------------------|  
|CREATE TABLE *nome-tabella di base*<br /><br /> (*tipo di dati identificatore di colonna*<br /><br /> [NON NULL]<br /><br /> [,*tipo di dati identificatore di colonna*<br /><br /> [NON NULL] ...)|CREATE TABLE *TableName1* [NAME *LongTableName*]<br /><br /> (*NomeCampo1* *TipoCampo*<br /><br /> [(*nLarghezzaCampo* [, *nPrecision*])]<br /><br /> [NON NULL])|  
  
 Quando si crea una tabella utilizzando il driver, il driver chiude la tabella immediatamente dopo la creazione per consentire l'accesso alla tabella da parte di altri utenti. Questo differisce da Visual FoxPro, che lascia il tavolo aperto esclusivamente al momento della creazione. Tuttavia, se viene eseguita una stored procedure nell'origine dati contenente un'istruzione CREATE TABLE, la tabella viene lasciata aperta.  
  
 Se l'origine dati è un database (file con estensione dbc), il driver ODBC di Visual FoxPro crea una tabella denominata *LongTableName* con lo stesso nome del *nome della tabella di base*.  
  
### <a name="using-data-definition-language-ddl"></a>Utilizzo del linguaggio DDL (Data Definition Language)  
 Non è possibile includere DDL nelle posizioni seguenti:  
  
-   In un'istruzione SQL batch che richiede una transazione  
  
-   In modalità di commit manuale, dopo un'istruzione che richiede una transazione, a meno che l'applicazione non chiami prima **SQLTransact**.  
  
 Ad esempio, se si desidera creare una tabella temporanea, è necessario creare la tabella prima di iniziare l'istruzione che richiede una transazione. Se si include l'istruzione CREATE TABLE in un'istruzione SQL batch che richiede una transazione, il driver restituisce un messaggio di errore.  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER TABLE - Comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Tipi di dati supportati (driver ODBC Visual FoxPro)](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [INSERT - Comando SQL](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT (comando SQL)](../../odbc/microsoft/select-sql-command.md)
