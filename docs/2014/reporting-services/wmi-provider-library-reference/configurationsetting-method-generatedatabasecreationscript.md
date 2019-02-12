---
title: Metodo GenerateDatabaseCreationScript (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- GenerateDatabaseCreationScript (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- GenerateDatabaseCreationScript method
ms.assetid: 25232dc7-00fe-4cd1-8a1c-7e36d552de00
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d2dbd112c340662ed90632a06904c0b3bd1939a3
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56022112"
---
# <a name="generatedatabasecreationscript-method-wmi-msreportserverconfigurationsetting"></a>Metodo GenerateDatabaseCreationScript (MSReportServer_ConfigurationSetting WMI)
  Genera uno script SQL che può essere utilizzato per creare un database del server di report.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub GenerateDatabaseCreationScript(ByVal DatabaseName As String, _  
    ByVal Lcid As Int32, ByVal IsSharePointMode As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseCreationScript(string DatabaseName, Int32 Lcid,   
    Boolean IsSharePointMode, out string Script, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *Databasename*  
 Stringa che contiene il nome del database del server di report da creare.  
  
 *LCID*  
 Valore utilizzato per localizzazione dei nomi di ruolo.  
  
 *IsSharePointMode*  
 Indica se creare database in modalità nativa o in modalità SharePoint.  
  
> [!IMPORTANT]  
>  A partire [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], *IsSharePointMode* = `True` non è supportata perché in modalità SharePoint, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è SharePoint un servizio condiviso e non è controllato dal provider WMI. Questo parametro deve essere impostato sempre su `False`.  
  
 *Script*  
 [out] Stringa che contiene lo script SQL generato.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Un valore pari a 0 indica l'esito positivo della chiamata al metodo. Un valore diverso da zero indica che si è verificato un errore.  
  
## <a name="remarks"></a>Note  
 Questo metodo genera uno script SQL che crea database del server di report per la versione del server di report attualmente connessa.  
  
 Il valore fornito nel parametro *DatabaseName* deve essere conforme alle convenzioni di denominazione dei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Il metodo non verifica l'esistenza del database al momento della generazione dello script.  
  
 Questo metodo non verifica l'esistenza del database del server di report al momento della generazione dello script.  
  
 Lo script generato supporta [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 e [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
