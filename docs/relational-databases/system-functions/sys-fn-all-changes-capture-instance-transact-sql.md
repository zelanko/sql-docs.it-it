---
title: sys. fn_all_changes_&lt;capture_instance&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_all_changes
- sys.fn_all_changes
- fn_all_changes_TSQL
- sys.fn_all_changes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_all_changes_<capture_instance>
- sys.fn_all_changes_<capture_instance>
ms.assetid: 564fae96-b88c-4f22-9338-26ec168ba6f5
author: rothja
ms.author: jroth
ms.openlocfilehash: 6b9b6e62d0f69c5182ad69e21cb46800d4ddcc86
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909393"
---
# <a name="sysfn_all_changes_ltcapture_instancegt-transact-sql"></a>sys.fn_all_changes_&lt;capture_instance&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wrapper per le funzioni di query di **tutte le modifiche** . Gli script necessari per creare queste funzioni vengono generati dalla stored procedure sys.sp_cdc_generate_wrapper_function.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn_all_changes_<capture_instance> ('start_time' ,'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all update old  
}  
```  
  
## <a name="arguments"></a>Argomenti  
 *start_time*  
 Valore **DateTime** che rappresenta l'endpoint inferiore dell'intervallo delle voci della tabella delle modifiche da includere nel set di risultati.  
  
 Nel set di risultati vengono incluse solo le righe della tabella delle modifiche CDC. < capture_instance > _CT con un'ora di commit associata maggiore di *start_time* .  
  
 Se viene fornito un valore NULL per questo argomento, l'endpoint inferiore dell'intervallo della query corrisponderà all'endpoint inferiore dell'intervallo valido per l'istanza di acquisizione.  
  
 *end_time*  
 Valore **DateTime** che rappresenta l'endpoint superiore dell'intervallo delle voci della tabella delle modifiche da includere nel set di risultati.  
  
 Questo parametro può assumere uno dei due possibili significati a seconda del valore scelto per @closed_high_end_point quando viene chiamato sys. sp_cdc_generate_wrapper_function per generare lo script di creazione per la funzione wrapper:  
  
-   @closed_high_end_point = 1  
  
     Nel set di risultati sono incluse solo le righe della tabella delle modifiche CDC. < capture_instance > _CT con un'ora di commit associata minore o uguale a end_time.  
  
-   @closed_high_end_point = 0  
  
     Nel set di risultati vengono incluse solo le righe della tabella delle modifiche CDC. capture_instance_CT a cui è associata un'ora di commit strettamente inferiore a end_time.  
  
 Se viene fornito un valore NULL per questo argomento, l'endpoint superiore dell'intervallo della query corrisponderà all'endpoint superiore dell'intervallo valido per l'istanza di acquisizione.  
  
 < row_filter_option >:: = {All | All Update Old}  
 Opzione applicata al contenuto delle colonne dei metadati e alle righe restituite nel set di risultati.  
  
 Le opzioni possibili sono le seguenti:  
  
 all  
 Restituisce tutte le modifiche all'interno dell'intervallo LSN specificato. Per le modifiche dovute a un'operazione di aggiornamento, questa opzione restituisce solo la riga che contiene i nuovi valori dopo l'applicazione dell'aggiornamento.  
  
 all update old  
 Restituisce tutte le modifiche all'interno dell'intervallo LSN specificato. Per le modifiche dovute a un'operazione di aggiornamento, questa opzione restituisce le due righe che contengono i valori della colonna prima e dopo l'aggiornamento.  
  
## <a name="table-returned"></a>Tabella restituita  
  
|Nome colonna|Tipo di colonna|Description|  
|-----------------|-----------------|-----------------|  
|__CDC_STARTLSN|**binary(10)**|Valore LSN di commit per la transazione associata alla modifica. Tutte le modifiche di cui è stato eseguito il commit nella stessa transazione condividono lo stesso valore LSN di commit.|  
|__CDC_SEQVAL|**binary(10)**|Valore di sequenza utilizzato per ordinare le modifiche alle righe in una transazione.|  
|\<colonne da @column_list|**varia**|Colonne identificate nell'argomento *column_list* per sp_cdc_generate_wrapper_function quando viene chiamata per generare lo script che crea la funzione wrapper.|  
|__CDC_OPERATION|**nvarchar(2)**|Codice operativo che indica l'operazione necessaria per applicare la riga all'ambiente di destinazione. Può variare in base al valore dell'argomento *row_filter_option* specificato nella chiamata:<br /><br /> *row_filter_option* =' all'<br /><br /> 'D' - operazione di eliminazione<br /><br /> 'I' - operazione di inserimento<br /><br /> 'UN' - operazione di aggiornamento ai nuovi valori<br /><br /> *row_filter_option* =' tutti gli aggiornamenti obsoleti '<br /><br /> 'D' - operazione di eliminazione<br /><br /> 'I' - operazione di inserimento<br /><br /> 'UN' - operazione di aggiornamento ai nuovi valori<br /><br /> 'UO' - operazione di aggiornamento ai valori obsoleti|  
|\<colonne da @update_flag_list|**bit**|Un flag di bit viene denominato aggiungendo _uflag al nome della colonna. Il flag viene sempre impostato su NULL quando \__CDC_OPERATION è' d',' I ', di ' UO '. Quando \__CDC_OPERATION è' UN', viene impostato su 1 se l'aggiornamento ha prodotto una modifica alla colonna corrispondente. Altrimenti, è impostato su 0.|  
  
## <a name="remarks"></a>Remarks  
 La funzione di > fn_all_changes_ < capture_instance funge da wrapper per la funzione di query CDC. fn_cdc_get_all_changes_ < capture_instance >. La stored procedure sys.sp_cdc_generate_wrapper viene utilizzata per generare lo script di creazione del wrapper.  
  
 Le funzioni wrapper non vengono create automaticamente. Per creare le funzioni wrapper, è necessario eseguire due operazioni:  
  
1.  Eseguire la stored procedure per generare lo script di creazione del wrapper.  
  
2.  Eseguire lo script per creare effettivamente la funzione wrapper.  

 Le funzioni wrapper consentono agli utenti di eseguire sistematicamente query per le modifiche apportate all'interno di un intervallo delimitato da valori **DateTime** anziché da valori LSN. Le funzioni wrapper eseguono tutte le conversioni necessarie tra i valori **DateTime** forniti e i valori LSN necessari internamente come argomenti per le funzioni di query. Quando le funzioni wrapper vengono utilizzate in modo seriale per elaborare un flusso di dati delle modifiche, assicurano che i dati non vengano persi o ripetuti a condizione che venga seguita la convenzione seguente: il valore @end_time dell'intervallo associato a una chiamata viene fornito come @start_time valore per l'intervallo associato alla chiamata successiva.  
  
 Utilizzando il parametro @closed_high_end_point durante la creazione dello script, è possibile generare wrapper per supportare un limite superiore chiuso o un limite superiore aperto nella finestra della query specificata, ovvero è possibile decidere se le voci che dispongono di un'ora di commit uguale al limite superiore dell'intervallo di estrazione devono essere incluse nell'intervallo. Per impostazione predefinita, il limite superiore è incluso.  
  
 Il set di risultati restituito dalla funzione wrapper **All Changes** restituisce rispettivamente le colonne _ _ $ start_lsn e \_\_$seqval della tabella delle modifiche come colonne \__CDC_STARTLSN e \__CDC_SEQVAL. Segue solo le colonne rilevate visualizzate nel parametro *\@column_list* al momento della generazione del wrapper. Se *\@column_list* è null, vengono restituite tutte le colonne di origine rilevate. Le colonne di origine sono seguite da una colonna operation, \__CDC_OPERATION, che è una colonna a uno o due caratteri che identifica l'operazione.  
  
 I flag di bit vengono quindi aggiunti al set di risultati per ogni colonna identificata nel parametro @update_flag_list. Per il wrapper **All Changes** , i flag di bit saranno sempre null se __CDC_OPERATION è' d',' I ' o ' UO '. Se \__CDC_OPERATION è' UN', il flag verrà impostato su 1 o 0, a seconda che l'operazione di aggiornamento abbia causato o meno una modifica alla colonna.  
  
 Il modello di configurazione di Change Data Capture ' Instantiate CDC wrapper funzioni con valori for schema ' Mostra come utilizzare sp_cdc_generate_wrapper_function stored procedure per ottenere gli script di creazione per tutte le funzioni wrapper per le funzioni di query definite di uno schema. Il modello crea quindi tali script. Per ulteriori informazioni sui modelli, vedere [Esplora modelli](../../ssms/template/template-explorer.md).  
  
## <a name="see-also"></a>Vedere anche  
 [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
