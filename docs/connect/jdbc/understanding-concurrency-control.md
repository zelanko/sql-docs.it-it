---
title: Informazioni sul controllo della concorrenza | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 98b7dabe-9b12-4e1d-adeb-e5b5cb0c96f3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3cbc805ece4cc28a646d93d6607bcc45d65cd563
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "69027642"
---
# <a name="understanding-concurrency-control"></a>Informazioni sul controllo della concorrenza
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Per controllo della concorrenza si intendono le diverse tecniche utilizzate per mantenere l'integrità del database quando più utenti aggiornano le righe contemporaneamente. Una concorrenza non corretta può causare problemi come letture dirty, letture fantasma e letture non ripetibili. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornisce interfacce per tutte le tecniche di concorrenza usate da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per risolvere questi problemi.  
  
> [!NOTE]  
>  Per altre informazioni sulla concorrenza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere "Gestione dell'accesso ai dati simultaneo" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Osservazioni  
 Il driver JDBC supporta i tipi di concorrenza seguenti:  
  
|Tipo di concorrenza|Caratteristiche|Blocchi di riga|Descrizione|  
|----------------------|---------------------|---------------|-----------------|  
|CONCUR_READ_ONLY|Sola lettura|No|Gli aggiornamenti eseguiti tramite il cursore non sono consentiti e sulle righe del set di risultati non viene mantenuto attivo alcun blocco.|  
|CONCUR_UPDATABLE|Ottimistica di lettura e scrittura|No|Si presuppone che le contese tra le righe nel database siano improbabili, ma possibili. L'integrità delle righe viene verificata tramite confronto del timestamp.|  
|CONCUR_SS_SCROLL_LOCKS|Pessimistica di lettura e scrittura|Sì|Si presuppone che le contese tra le righe nel database siano probabili. L'integrità delle righe viene assicurata tramite i blocchi di riga.|  
|CONCUR_SS_OPTIMISTIC_CC|Ottimistica di lettura e scrittura|No|Si presuppone che le contese tra le righe nel database siano improbabili, ma possibili. L'integrità delle righe viene verificata tramite confronto del timestamp.<br /><br /> In [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive, il server modifica questa impostazione in CONCUR_SS_OPTIMISTIC_CCVAL se nella tabella non è presente una colonna timestamp.<br /><br /> In [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], se nella tabella sottostante è presente una colonna timestamp, viene usata l'opzione OPTIMISTIC WITH ROW VERSIONING anche se è specificata l'opzione OPTIMISTIC WITH VALUES. Se si specifica l'opzione OPTIMISTIC WITH ROW VERSIONING e nella tabella non sono incluse colonne timestamp, viene utilizzata l'opzione OPTIMISTIC WITH VALUES.|  
|CONCUR_SS_OPTIMISTIC_CCVAL|Ottimistica di lettura e scrittura|No|Si presuppone che le contese tra le righe nel database siano improbabili, ma possibili. L'integrità delle righe viene verificata tramite confronto dei dati della riga.|  
  
## <a name="result-sets-that-are-not-updateable"></a>Set di risultati non aggiornabili  
 Un set di risultati aggiornabile è un set di risultati in cui è possibile inserire, aggiornare ed eliminare righe. Nei casi seguenti, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non può creare un cursore aggiornabile e viene generata l'eccezione "Il set di risultati non è aggiornabile".  
  
|Causa|Descrizione|Rimedio|  
|-----------|-----------------|------------|  
|L'istruzione non viene creata utilizzando la sintassi JDBC 2.0 (o versioni successive)|In JDBC 2.0 sono stati introdotti nuovi metodi per la creazione di istruzioni. Se viene utilizzata la sintassi JDBC 1.0, il set di risultati per impostazione predefinita è di sola lettura.|Specificare il tipo di set di risultati e la concorrenza in fase di creazione dell'istruzione.|  
|L'istruzione viene creata utilizzando TYPE_SCROLL_INSENSITIVE|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea un cursore snapshot statico. Il cursore è disconnesso dalle righe della tabella sottostante per proteggerlo dagli aggiornamenti apportati alle righe da altri utenti.|Utilizzare TYPE_SCROLL_SENSITIVE, TYPE_SS_SCROLL_KEYSET, TYPE_SS_SCROLL_DYNAMIC o TYPE_FORWARD_ONLY con CONCUR_UPDATABLE per evitare di creare un cursore statico.|  
|La struttura della tabella non consente un cursore di tipo KEYSET o DYNAMIC|La tabella sottostante non contiene chiavi univoche per consentire a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di identificare in modo univoco una riga.|Aggiungere chiavi univoche alla tabella per consentire l'identificazione univoca di ogni riga.|  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione dei set di risultati con il driver JDBC](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
