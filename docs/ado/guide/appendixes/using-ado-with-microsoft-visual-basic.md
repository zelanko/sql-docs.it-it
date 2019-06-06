---
title: Uso di ADO con Microsoft Visual Basic | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, Visual Basic
- Visual Basic [ADO]
ms.assetid: 9dfb6784-037d-4f9d-bb7f-b506b4498573
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: abbdbeec81a029716ac6516f9436373e91365a23
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702781"
---
# <a name="using-ado-with-microsoft-visual-basic-and-visual-basic-for-applications"></a>Uso di ADO con Microsoft Visual Basic e Visual Basic for Applications
Configurazione di un progetto di ADO e la scrittura di codice ADO è simile se si usa Visual Basic o Visual Basic per le applicazioni. In questo argomento risolve l'uso di ADO con Visual Basic e Visual Basic per le applicazioni e note eventuali differenze.

## <a name="referencing-the-ado-library"></a>Riferimento alla libreria ADO
 La libreria ADO deve fare riferimento al progetto.

#### <a name="to-reference-ado-from-microsoft-visual-basic"></a>Riferimento ADO di Microsoft Visual Basic

1.  In Visual Basic dal **Project** dal menu **riferimenti...** .

2.  Selezionare **x.x. Microsoft ActiveX Data Objects libreria** dall'elenco. Verificare che almeno risulteranno selezionate anche le librerie seguenti:

    -   Visual Basic, Applications Edition

    -   Procedure e gli oggetti di runtime di Visual Basic

    -   Procedure e oggetti di Visual Basic

    -   automazione OLE

3.  Fare clic su **OK**.

 È possibile utilizzare ADO altrettanto facilmente con Visual Basic per le applicazioni, usando ad esempio Microsoft Access.

#### <a name="to-reference-ado-from-microsoft-access"></a>Riferimento ADO da Microsoft Access

1.  In Microsoft Access, selezionare o creare un modulo dal **moduli** scheda le **Database** finestra.

2.  Nel **degli strumenti** dal menu **riferimenti...** .

3.  Selezionare **x.x. Microsoft ActiveX Data Objects libreria** dall'elenco. Verificare che almeno risulteranno selezionate anche le librerie seguenti:

    -   Visual Basic, Applications Edition

    -   Libreria oggetti di Microsoft Access 8.0 (o versioni successive)

    -   Libreria oggetti Microsoft DAO 3.5 (o versioni successive)

4.  Fare clic su **OK**.

## <a name="creating-ado-objects-in-visual-basic"></a>Creazione di oggetti ADO in Visual Basic
 Per creare una variabile di automazione e un'istanza di un oggetto per tale variabile, è possibile utilizzare due metodi: **Dim** oppure **CreateObject**.

### <a name="dim"></a>Dim
 È possibile usare la **New** parola chiave with **Dim** dichiarare e creare istanze di oggetti ADO in un unico passaggio:

```
Dim conn As New ADODB.Connection
```

 In alternativa, il **Dim** creazione dell'istanza dichiarazione e l'oggetto istruzione può anche essere due passaggi:

```
Dim conn As ADODB.Connection
Set conn = New ADODB.Connection
```

> [!NOTE]
>  Non è necessario usare in modo esplicito il `ADODB` progid con il **Dim** istruzione, presupponendo che si è fatto riferimento alla libreria ADO correttamente nel progetto. Tuttavia, usarlo assicura che non è in conflitto con altre librerie di denominazione.

> [!NOTE]
>  Ad esempio, se si includono riferimenti a ADO e DAO nello stesso progetto, si deve includere un qualificatore per specificare quale modello di oggetto da utilizzare per creare un'istanza **Recordset** oggetti, come nel codice seguente:

```
Dim adoRS As ADODB.Recordset
Dim daoRS As DAO.Recordset
```

### <a name="createobject"></a>CreateObject
 Con il **CreateObject** creazione dell'istanza (metodo), la dichiarazione e l'oggetto deve essere due passaggi discreti:

```
Dim conn1
Set conn1 = CreateObject("ADODB.Connection") As Object
```

 Creare istanze degli oggetti con **CreateObject** sono con associazione tardiva, il che significa che non sono fortemente tipizzati e completamento tramite la riga di comando è disabilitato. Tuttavia, consentono di ignorare la libreria ADO di riferimento dal progetto e consente di creare un'istanza di versioni specifiche di oggetti. Ad esempio:

```
Set conn1 = CreateObject("ADODB.Connection.2.0") As Object
```

 È anche possibile eseguire questa operazione in modo specifico la creazione di un riferimento alla libreria ADO versione 2.0 di tipo e la creazione dell'oggetto.

 Creando istanze di oggetti utilizzando il **CreateObject** metodo è in genere più lento rispetto all'uso di **Dim** istruzione.

## <a name="handling-events"></a>Gestione degli eventi
 Per gestire eventi ADO in Microsoft Visual Basic, è necessario dichiarare una variabile di a livello di modulo usando il **WithEvents** (parola chiave). La variabile può essere dichiarata solo come parte di un modulo di classe e deve essere dichiarata a livello di modulo. Per una discussione più approfondita della gestione degli eventi ADO, vedere [gestione degli eventi ADO](../../../ado/guide/data/handling-ado-events.md).

## <a name="visual-basic-examples"></a>Esempi di Visual Basic
 Molti esempi di Visual Basic sono inclusi nella documentazione di ADO. Per altre informazioni, vedere [esempi di codice ADO in Microsoft Visual Basic](../../../ado/reference/ado-api/ado-code-examples-in-visual-basic.md).

## <a name="see-also"></a>Vedere anche
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md) [uso di ADO con Microsoft Visual C++](../../../ado/guide/appendixes/using-ado-with-microsoft-visual-c.md) [uso di ADO con linguaggi di Scripting](../../../ado/guide/appendixes/using-ado-with-scripting-languages.md)
