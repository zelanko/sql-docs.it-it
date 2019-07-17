---
title: Uso delle estensioni di Visual C++ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ [ADO], using VC++ extensions
- ADO, Visual C++
ms.assetid: ff759185-df41-4507-8d12-0921894ffbd9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a9d60695bd033bfc83e3a091490f27f9432782c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926459"
---
# <a name="visual-c-extensions"></a>Estensioni di Visual C++
## <a name="the-iadorecordbinding-interface"></a>L'interfaccia IADORecordBinding
 Le estensioni di Microsoft Visual C++ per ADO associano, o binding, i campi di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto alle variabili di C/C++. Ogni volta che la riga corrente del limite **Recordset** cambia, tutti i campi associati nel **Recordset** vengono copiate le variabili di C/C++. Se necessario, i dati copiati viene convertiti nel tipo di dati dichiarato della variabile di C/C++.

 Il **BindToRecordset** metodo per il **IADORecordBinding** interfaccia campi vengono associati alle variabili di C/C++. Il **AddNew** metodo aggiunge una nuova riga al limite **Recordset**. Il **Update** metodo popola i campi in nuove righe delle **Recordset**, o ne aggiorna i campi nelle righe esistenti, con il valore delle variabili di C/C++.

 Il **IADORecordBinding** viene implementata mediante il **Recordset** oggetto. Non codificare l'implementazione.

## <a name="binding-entries"></a>Voci di associazione
 Le estensioni di Visual C++ per ADO mappare i campi di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto alle variabili di C/C++. La definizione di un mapping di un campo a una variabile viene chiamata un *associazione di voce*. Macro di forniscono le voci di associazione di dati numerici a lunghezza fissa e a lunghezza variabile. Le voci di associazione e le variabili di C/C++ vengono dichiarate in una classe derivata dalla classe di estensioni di Visual C++ **CADORecordBinding**. Il **CADORecordBinding** classe è definita internamente dalle macro di ingresso di associazione.

 ADO esegue il mapping internamente i parametri in queste macro per OLE DB **DBBINDING** strutturare e crea OLE DB **della funzione di accesso** oggetto per gestire lo spostamento e la conversione dei dati tra i campi e variabili. OLE DB definisce i dati, costituito da tre parti: Oggetto *buffer* indica dove sono archiviati i dati; un *stato* che indica se un campo è stato correttamente archiviato nel buffer, o il modo in cui la variabile deve essere ripristinata al campo; e *lunghezza* dei dati. (Vedere [introduzione e l'impostazione dei dati (OLE DB)](https://msdn.microsoft.com/4369708b-c9fb-4d48-a321-bf949b41a369)nel riferimento delle per programmatori OLE DB, per altre informazioni.)

## <a name="header-file"></a>File di intestazione
 Nell'applicazione per poter usare le estensioni di Visual C++ per ADO, includere il file seguente:

```cpp
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>Associazione dei campi del Recordset

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>Per associare i campi del Recordset alle variabili di C/C++

1.  Creare una classe derivata dal **CADORecordBinding** classe.

2.  Specificare le voci di associazione e le variabili di C/C++ corrispondente nella classe derivata. Racchiudere tra parentesi quadre le voci di associazione tra **le macro BEGIN_ADO_BINDING** e **END_ADO_BINDING** macro. Non terminare le macro con virgole o punti e virgola. Delimitatori appropriati vengono specificati automaticamente da tutte le macro.

     Specificare una voce di associazione per ogni campo può essere mappata a una variabile di C/C++. Un membro appropriato da usare la **ADO_FIXED_LENGTH_ENTRY**, **ADO_NUMERIC_ENTRY**, o **ADO_VARIABLE_LENGTH_ENTRY** della famiglia di macro.

3.  Nell'applicazione, creare un'istanza della classe derivata da **CADORecordBinding**. Ottenere il **IADORecordBinding** dell'interfaccia dalle **Recordset**. Chiamare quindi il **BindToRecordset** metodo a cui associare il **Recordset** campi alle variabili di C/C++.

 Per altre informazioni, vedere la [esempio di estensioni di Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md).

## <a name="interface-methods"></a>Metodi di interfaccia
 Il **IADORecordBinding** interfaccia dispone di tre metodi: **BindToRecordset**, **AddNew**, e **Update**. L'unico argomento per ogni metodo è un puntatore a un'istanza della classe derivata da **CADORecordBinding**. Pertanto, il **AddNew** e **Update** metodi non possono specificare uno dei parametri dei relativi omonimi ADO.

## <a name="syntax"></a>Sintassi
 Il **BindToRecordset** metodo associa il **Recordset** campi con le variabili di C/C++.

```cpp
BindToRecordset(CADORecordBinding *binding)
```

 Il **AddNew** metodo richiama il relativo omonimo, ADO [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) metodo, aggiungere una nuova riga per il **Recordset**.

```cpp
AddNew(CADORecordBinding *binding)
```

 Il **aggiornare** metodo richiama il relativo omonimo, ADO [aggiornare](../../../ado/reference/ado-api/update-method.md) metodo, per aggiornare il **Recordset**.

```cpp
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>Macro di voci di associazione
 Macro di voci di associazione definiscono l'associazione di un **Recordset** campo e una variabile. Una macro di inizio e fine delimita il set di voci di associazione.

 Famiglie di macro vengono fornite per i dati a lunghezza fissa, ad esempio **adDate** oppure **adBoolean**; numerico i dati, ad esempio **adTinyInt**, **tutti**, oppure **adDouble**; e i dati a lunghezza variabile, ad esempio **famiglia**, **adVarChar** oppure **adVarBinary**. Tutti i tipi numerici, ad eccezione di **adVarNumeric**, sono anche tipi a lunghezza fissa. Ogni famiglia è costituita da diversi set di parametri in modo che è possibile escludere le informazioni di associazione di alcun interesse.

 Per altre informazioni, vedere [appendice a: Tipi di dati](https://msdn.microsoft.com/e3a0533a-2196-4eb0-a31e-92fe9556ada6), di riferimento per programmatori OLE DB.

### <a name="begin-binding-entries"></a>Iniziare a voci di associazione
 **Le macro BEGIN_ADO_BINDING**(*classe*)

### <a name="fixed-length-data"></a>Dati a lunghezza fissa
 **ADO_FIXED_LENGTH_ENTRY**(*ordinale, tipo di dati, Buffer, lo stato, modificare*)

 **ADO_FIXED_LENGTH_ENTRY2**(*ordinale, tipo di dati, del Buffer, modificare*)

### <a name="numeric-data"></a>Dati numerici
 **ADO_NUMERIC_ENTRY**(*ordinale, tipo di dati, Buffer, precisione, scala, lo stato, modificare*)

 **ADO_NUMERIC_ENTRY2**(*ordinale, tipo di dati, Buffer, precisione, scala, modificare*)

### <a name="variable-length-data"></a>Dati a lunghezza variabile
 **ADO_VARIABLE_LENGTH_ENTRY**(*ordinale, tipo di dati, Buffer, le dimensioni, lo stato, lunghezza, modificare*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*ordinale, tipo di dati, Buffer, le dimensioni, lo stato, modificare*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*ordinale, tipo di dati, Buffer, le dimensioni, lunghezza, modificare*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*ordinale, tipo di dati, Buffer, le dimensioni, modificare*)

### <a name="end-binding-entries"></a>Associazione voci finali
 **END_ADO_BINDING**()

|Parametro|Descrizione|
|---------------|-----------------|
|*Classe*|Classe in cui sono definite le voci di associazione e le variabili di C/C++.|
|*Ordinal*|Numero ordinale a partire da uno, del **Recordset** campo corrispondente alla variabile di C/C++.|
|*DataType*|Tipo di dati ADO equivalente della variabile di C/C++ (vedere [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) per un elenco di tipi di dati validi). Il valore della **Recordset** campo verrà convertito in questo tipo di dati se necessario.|
|*Buffer*|Nome della variabile C/C++ in cui il **Recordset** campo verrà archiviato.|
|*Dimensione*|Dimensioni massime in byte del *Buffer*. Se *Buffer* conterrà una stringa a lunghezza variabile, consentire spazio per un terminazione zero.|
|*Status*|Nome di una variabile che indica se il contenuto del *Buffer* validi e se la conversione del campo da *DataType* ha avuto esito positivo.<br /><br /> I due valori più importanti per questa variabile sono **adFldOK**, ovvero la conversione ha avuto esito positivo; e **adFldNull**, ovvero il valore del campo sarebbe una variante di tipo VT_NULL e non semplicemente vuoto.<br /><br /> I possibili valori per *stato* sono elencati nella tabella seguente, "Valori dello stato".|
|*Modificare*|Flag booleano. Se TRUE, indica ad ADO è consentito aggiornare corrispondente **Recordset** con il valore contenuto nel campo *Buffer*.<br /><br /> Impostare il valore booleano *modificare* parametro su TRUE per abilitare ADO aggiornare il campo associato e FALSE se si desidera esaminare il campo, ma non modificarlo.|
|*Precisione*|Numero di cifre che può essere rappresentato in una variabile numerica.|
|*Scala*|Numero di posizioni decimali in una variabile numerica.|
|*Lunghezza*|Nome di una variabile a quattro byte che contiene la lunghezza effettiva dei dati in *Buffer*.|

## <a name="status-values"></a>Valori di stato
 Il valore della *stato* variabile indica se un campo è stato correttamente copiato a una variabile.

 Quando si impostano i dati, *lo stato* può essere impostato su **adFldNull** per indicare il **Recordset** campo deve essere impostato su null.

|Costante|Value|Descrizione|
|--------------|-----------|-----------------|
|**adFldOK**|0|È stato restituito un valore del campo non null.|
|**adFldBadAccessor**|1|Associazione non è valida.|
|**adFldCantConvertValue**|2|Valore non è stato convertito per motivi diversi da overflow o non corrispondenza di segno.|
|**adFldNull**|3|Quando si recupera un campo, indica che è stato restituito un valore null.<br /><br /> Quando si imposta un campo, indica il campo deve essere impostato su **NULL** quando non è possibile codificare il campo **NULL** stesso (ad esempio, una matrice di caratteri o un numero intero).|
|**adFldTruncated**|4|Dati a lunghezza variabile o valori numerici sono stati troncati.|
|**adFldSignMismatch**|5|Valore è con segno mentre il tipo di dati della variabile è senza segno.|
|**adFldDataOverFlow**|6|Il valore è maggiore di possono essere archiviati nel tipo di dati della variabile.|
|**adFldCantCreate**|7|Tipo di colonna sconosciuto e il campo è già aperta.|
|**adFldUnavailable**|8|Valore del campo non è stato possibile determinare ad esempio, su un campo di nuovo, non assegnato non prevede alcun valore predefinito.|
|**adFldPermissionDenied**|9|Quando non si aggiorna, nessuna autorizzazione per scrivere i dati.|
|**adFldIntegrityViolation**|10|Durante l'aggiornamento, il valore del campo violerebbe l'integrità della colonna.|
|**adFldSchemaViolation**|11|Durante l'aggiornamento, il valore del campo violerebbe dello schema di colonna.|
|**adFldBadStatus**|12|Quando si aggiorna, parametro di stato non valido.|
|**adFldDefault**|13|Durante l'aggiornamento, è stato usato un valore predefinito.|

## <a name="see-also"></a>Vedere anche
 [Esempio di estensioni di Visual C++](../../../ado/guide/appendixes/visual-c-extensions-example.md) [intestazione delle estensioni di Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)
