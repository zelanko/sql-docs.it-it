---
title: Metodo ListSSLCertificateBindings (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListSSLCertificateBindings method
ms.assetid: d12d280c-9b6f-47a8-bcd9-34cde31c8886
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0a2a33d7aa992fd434b29fd519c805f57b2b46fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66098354"
---
# <a name="listsslcertificatebindings-method-wmi-msreportserver_configurationsetting"></a>Metodo ListSSLCertificateBindings (MSReportServer_ConfigurationSetting WMI)
  Restituisce un elenco dei certificati SSL installati presenti nel computer.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub ListSSLCertificateBindings(ByVal LCID As Int32, ByRef Application() As String, _  
    ByRef CertificateHash() As String, ByRef IPAddresses() As String, ByRef Port() As Int32, _  
    ByRef Errors() As String, ByRef Length As Int32, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListSSLCertificateBindings(Int32 Lcid, out string[] Application,   
    out string[] CertificateHash,out string[] IPAddress,   
    out Int32[] Port, out string Errors,   
    out Int32 length, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *LCID*  
 Impostazioni locali da utilizzare per i messaggi di errore restituiti.  
  
 *Applicazione []*  
 [out] Applicazioni che dispongono di associazioni certificato.  
  
 *CertificateHash []*  
 [out] Hash per i certificati.  
  
 *IPAddress []*  
 [out] Indirizzo IP per le applicazioni.  
  
 *Porta []*  
 [out] Numero di porta archiviato nell'associazione in rsreportserver.config.  
  
 *Errori []*  
 [out] Descrizioni degli errori che si sono verificati.  
  
 *Length*  
 [out] Lunghezza della matrice restituita dal metodo.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Un valore pari a 0 indica l'esito positivo della chiamata al metodo. Un valore diverso da zero indica che si è verificato un errore.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:**[!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
