---
title: IBCPSession (OLE DB Driver) | Microsoft Docs
description: Informazioni su come OLE DB Driver per SQL Server usa IBCPSession per supportare le operazioni di copia bulk basate su file SQL Server e sui relativi membri.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IBCPSession interface
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d00a0bff09785fde1c27b89426ca680b2a0f889
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861915"
---
# <a name="ibcpsession-ole-db"></a>IBCPSession (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  L'interfaccia **IBCPSession** espone il supporto per le operazioni di copia bulk basate su file [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. L'interfaccia **IBCPSession** viene esposta in OLE DB Driver per SQL Server nello stesso livello degli oggetti Session. Nel driver OLE DB per SQL Server, gli oggetti origine dati sono factory per gli oggetti Session e le operazioni di copia bulk vengono specificate nella proprietà di connessione SSPROP_ENABLEBULKCOPY. Inoltre, la proprietà SSPROP_ENABLEFASTLOAD deve essere impostata su True.  
  
 La chiamata al metodo **IDBCreateSession::CreateSession** comporterà quindi la creazione di un oggetto **BulkCopySession**. Tutti i metodi di copia bulk basati su file esposti tramite l'oggetto **IBCPSession** possono essere quindi chiamati con firme molto simili sull'interfaccia **IBCPSession** di questo oggetto **IBCPSession**.  
  
> [!NOTE]  
>  Il driver OLE DB per SQL Server supporta operazioni di copia bulk basate sulla memoria tramite l'interfaccia [IRowsetFastLoad](../../oledb/ole-db-interfaces/irowsetfastload-ole-db.md).  
  
 Per altre informazioni sull'uso di OLE DB Driver for SQL Server per le operazioni di copia bulk, vedere [Esecuzione di operazioni di copia bulk](../../oledb/features/performing-bulk-copy-operations.md).  
  
 Per un esempio che illustra come usare l'interfaccia **IBCPSession**, vedere [IBCPSession::BCPDone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[IBCPSession::BCPColFmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)|Crea un'associazione tra variabili di programma e colonne di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[IBCPSession::BCPColumns &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)|Imposta il numero di campi da associare alle colonne di una tabella di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[IBCPSession::BCPControl &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)|Imposta le opzioni per un'operazione di copia bulk.|  
|[IBCPSession::BCPDone &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)|Esegue il commit delle righe restanti da inviare a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[IBCPSession::BCPExec &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)|Esegue l'operazione di copia bulk.|  
|[IBCPSession::BCPInit &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)|Inizializza la struttura della copia bulk, esegue alcune operazioni di controllo degli errori, verifica che i dati e i nomi dei file di formato siano corretti, quindi li apre.|  
|[IBCPSession::BCPReadFmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)|Legge le informazioni sul formato per ogni colonna dal file di formato.|  
|[IBCPSession::BCPWriteFmt &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md)|Scrive informazioni sul formato per ogni colonna nel file di formato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Interfacce &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)  
  
  
