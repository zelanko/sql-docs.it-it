---
title: Un Provider Microsoft OLE DB semplice | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bc17df7bad00205803b33cb4af17cb3c6ddaac56
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701290"
---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Panoramica di Simple Provider Microsoft OLE DB
Il Microsoft OLE DB semplici Provider (OSP) consente di ADO accedere ai dati per il quale un provider è stata scritta usando la [OLE DB semplici Provider (OSP) Toolkit](https://msdn.microsoft.com/6e7b7931-9e4a-4151-ae51-672abd3f84a6). I provider di semplici sono utili per accedere alle origini dati che richiedono il supporto OLE DB solo fondamentale, ad esempio le matrici in memoria o documenti XML.

## <a name="connection-string-parameters"></a>Parametri della stringa di connessione
 Per connettersi a OLE DB semplici Provider DLL, impostare il *Provider* argomento per il [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) proprietà:

```vb
MSDAOSP
```

 Questo valore può anche essere impostato o letto usando il [Provider](../../../ado/reference/ado-api/provider-property-ado.md) proprietà.

 È possibile connettersi a un provider semplice che è stato registrato come provider OLE DB completo usando il nome del provider registrato, determinato dal writer del provider.

## <a name="typical-connection-string"></a>Stringa di connessione tipica
 Una stringa di connessione tipica per questo provider è:

```vb
"Provider=MSDAOSP;Data Source=serverName"
```

 La stringa è costituita da queste parole chiave:

|Parola chiave|Descrizione|
|-------------|-----------------|
|**Provider**|Specifica il provider OLE DB per SQL Server.|
|**Data Source**|Specifica il nome di un server.|

## <a name="xml-document-example"></a>Esempio di documento XML
 Di OLE DB semplici Provider (OSP) in MDAC 2.7 o versioni successive e Windows Data Access Components (Windows DAC) è stata migliorata per supportare l'apertura ADO gerarchica **recordset** rispetto ai file XML arbitrari. Questi file XML possono contenere lo schema di persistenza XML ADO, ma non è obbligatorio. Questa è stata implementata tramite la connessione di OSP per il **MSXML2.DLL**; pertanto **il file Msxml2.dll sia** o versione successiva è obbligatorio.

 Il **portfolio. XML** file usato nell'esempio seguente contiene la struttura seguente:

```console
Portfolio
   Stock
      Shares
      Symbol
      Price
      Info
         Company Name
         WebSite
```

 Gli oggetti DSO XML utilizza euristica incorporata per convertire i nodi in un albero XML in capitoli gerarchico **Recordset**.

 Usando questi euristica incorporata, l'albero XML viene convertito in un a due livelli gerarchici **Recordset** nel formato seguente:

```console
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 Si noti che i tag di Portfolio e informazioni non vengano rappresentati nella gerarchica **Recordset**. Per una spiegazione delle modalità di DSO XML di conversione degli alberi XML gerarchico **recordset**, vedere le seguenti regole. La colonna $Text è descritto nella sezione seguente.

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>Regole per l'assegnazione di elementi e attributi XML da colonne e righe
 Gli oggetti DSO XML segue una procedura per l'assegnazione di elementi e attributi alle colonne e righe nelle applicazioni con associazione a dati. XML viene modellato come un albero con un unico tag che contiene l'intera gerarchia. Ad esempio, una descrizione XML di un libro può contenere tag capitolo, figura tag e i tag di sezione. Il livello più alto sarà il tag della Rubrica, contenente il capitolo di sottoelementi, la figura e sezione. Quando gli oggetti DSO XML esegue il mapping di elementi XML in righe e colonne, i sottoelementi, non l'elemento di livello superiore, vengono convertiti.

 Gli oggetti DSO XML utilizza questa procedura per la conversione dei sottoelementi:

-   Ogni sottoelemento e attributo corrisponde a una colonna in alcune **Recordset** nella gerarchia.

-   Il nome della colonna è identico al nome del sottoelemento o attributo, a meno che l'elemento padre ha un attributo e un sottoelemento con lo stesso nome, nel qual caso un "!" viene anteposta al nome di colonna del sottoelemento.

-   Ogni colonna può essere un *semplice* colonna contiene valori scalari (in genere le stringhe) o una **Recordset** colonna che contiene figlio **recordset**.

-   Le colonne corrispondenti agli attributi sono sempre semplici.

-   Sono colonne corrispondono ai sottoelementi **Recordset** colonne se il sottoelemento ha un proprio sottoelementi o attributi (o entrambi), o padre del sottoelemento ha più di un'istanza del sottoelemento come elemento figlio. In caso contrario, la colonna è semplice.

-   Quando sono presenti più istanze di un sottoelemento (padri differenti), la relativa colonna è una **Recordset** colonna se *qualsiasi* delle istanze implica una **Recordset** colonna; relativo è semplice colonna solo se *tutti* istanze implicano una colonna semplice.

-   Tutti i **recordset** dispone di una colonna aggiuntiva denominata $Text.

 Il codice che serve per creare un **Recordset** è come segue:

```vb
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "https://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  Il percorso del file di dati può essere specificato usando quattro diverse convenzioni di denominazione.

```vb
'HTTP://
adoRS.Open "https://WebServer/VRoot/portfolio.xml", adoConn
'FILE://
adoRS.Open "file:/// C:\\Directory\\portfolio.xml", adoConn
'UNC Path
adoRS.Open "\\ComputerName\ShareName\portfolio.xml", adoConn
'Full DOS Path
adoRS.Open "C:\Directory\portfolio.xml", adoConn
```

 Non appena il **Recordset** è stato aperto, il consueto ADO **Recordset** comandi di navigazione possono essere utilizzati.

 **Recordset** generati dal OSP presentano alcune limitazioni:

-   I cursori client (**adUseClient**) non sono supportati.

-   Gerarchica **recordset** creati nel corso del arbitrario XML non può essere reso persistente utilizzando **Recordset. Save**.

-   **Recordset** creato con il OSP sono di sola lettura.

-   Il XMLDSO aggiunge una colonna aggiuntiva dei dati ($Text) a ognuno **Recordset** nella gerarchia.

 Per altre informazioni sui Provider OLE DB semplici, vedere [compilazione di un Provider semplice](https://msdn.microsoft.com/b31a6cba-58ae-4ee8-9039-700973d354d6).

## <a name="code-example"></a>Esempio di codice
 Il codice di Visual Basic seguente illustra l'apertura di un file XML arbitrario, costruzione di un modello gerarchico **Recordset**e in modo ricorsivo la scrittura di ogni record della ognuno **Recordset** alla finestra di debug.

 Ecco un semplice file XML che contiene le quotazioni di borsa. Il codice seguente usa questo file per costruire un a due livelli gerarchici **Recordset**.

```xml
<portfolio>
   <stock>
      <shares>100</shares>
      <symbol>MSFT</symbol>
      <price>$70.00</price>
      <info>
         <companyname>Microsoft Corporation</companyname>
         <website>https://www.microsoft.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>AAPL</symbol>
      <price>$107.00</price>
      <info>
         <companyname>Apple Computer, Inc.</companyname>
         <website>https://www.apple.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>DELL</symbol>
      <price>$50.00</price>
      <info>
         <companyname>Dell Corporation</companyname>
         <website>https://www.dell.com</website>
      </info>
    </stock>
    <stock>
       <shares>100</shares>
       <symbol>INTC</symbol>
       <price>$115.00</price>
       <info>
          <companyname>Intel Corporation</companyname>
          <website>https://www.intel.com</website>
       </info>
   </stock>
</portfolio>
```

 Di seguito sono sub (routine) due Visual Basic. La prima crea il **Recordset** e lo passa al *WalkHier* sub routine, illustra in modo che in modo ricorsivo verso il basso della gerarchia, la scrittura di ogni **campo** in ogni record in ogni **Recordset** alla finestra di debug.

```vb
Private Sub BrowseHierRecordset()
' Add ADO 2.7 or later to Project/References
' No need to add MSXML2, ADO just passes the ProgID through to the OSP.

    Dim adoConn As ADODB.Connection
    Dim adoRS As ADODB.Recordset
    Dim adoChildRS As ADODB.Recordset

    Set adoConn = New ADODB.Connection
    Set adoRS = New ADODB.Recordset
    Set adoChildRS = ADODB.Recordset

    adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
    adoRS.Open "https://bwillett3/Kowalski/portfolio.xml", adoConn

    Dim iLevel As Integer
    iLevel = 0
    WalkHier iLevel, adoRS

End Sub

Sub WalkHier(ByVal iLevel As Integer, ByVal adoRS As ADODB.Recordset)
    iLevel = iLevel + 1
    PriorLevel = iLevel
    While Not adoRS.EOF
        For ndx = 0 To adoRS.Fields.Count - 1
            If adoRS.Fields(ndx).Name <> "$Text" Then
                If adoRS.Fields(ndx).Type = adChapter Then
                    Set adoChildRS = adoRS.Fields(ndx).Value
                    WalkHier iLevel, adoChildRS
                Else
                    Debug.Print iLevel & ": adoRS.Fields(" & ndx & _
                       ") = " & adoRS.Fields(ndx).Name & " = " & _
                       adoRS.Fields(ndx).Value
                End If
            End If
        Next ndx
        adoRS.MoveNext
    Wend
    iLevel = PriorLevel
End Sub
```
