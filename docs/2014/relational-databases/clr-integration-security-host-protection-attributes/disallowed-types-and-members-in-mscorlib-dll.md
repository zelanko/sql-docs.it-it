---
title: Tipi e membri non consentiti in mscorlib.dll | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: daf82d4b-2f6d-44ca-9148-75193321b6d5
author: rothja
ms.author: jroth
ms.openlocfilehash: cc4e42a0f900231bdd28417420cdab19b7345e66
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954321"
---
# <a name="disallowed-types-and-members-in-mscorlibdll"></a>Tipi e membri non consentiti in mscorlib.dll
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la programmazione Common Language Integration (CLR) non consente l'utilizzo di un tipo o di un membro che dispone di un oggetto `HostProtectionAttribute` che specifica un' `System.Security.Permissions.HostProtectionResource` enumerazione con un valore `ExternalProcessMgmt` , `ExternalThreading` , `MayLeakOnAbort` , `SecurityInfrastructure` , `SelfAffectingProcessMgmnt` , `SelfAffectingThreading` , **SharedState**, `Synchronization` o `UI` . Nella tabella seguente sono elencati i membri e i tipi dell'assembly mscorlib.dll i cui valori degli attributi di protezione host non sono consentiti.  
  
> [!NOTE]  
>  Questo elenco è stato generato dagli assembly supportati. Per ulteriori informazioni, vedere [supported .NET Framework libraries](../clr-integration/database-objects/supported-net-framework-libraries.md).  
  
|Tipo o membro|Valori dell'attributo di protezione host|  
|--------------------|--------------------|  
|SyncStream.BeginRead()|ExternalThreading|  
|SyncStream.BeginWrite()|ExternalThreading|  
|System.Collections.ArrayList.Synchronized()|Sincronizzazione|  
|System.Collections.Hashtable.Synchronized()|Sincronizzazione|  
|System.Collections.Queue.Synchronized()|Sincronizzazione|  
|System.Collections.SortedList.Synchronized()|Sincronizzazione|  
|System.Collections.Stack.Synchronized()|Sincronizzazione|  
|System.Console.Beep()|Interfaccia utente|  
|System.Console.get_Error()|Interfaccia utente|  
|System.Console.get_In()|Interfaccia utente|  
|System.Console.get_KeyAvailable()|Interfaccia utente|  
|System.Console.get_Out()|Interfaccia utente|  
|System.Console.OpenStandardError()|Interfaccia utente|  
|System.Console.OpenStandardInput()|Interfaccia utente|  
|System.Console.OpenStandardOutput()|Interfaccia utente|  
|System.Console.Read()|Interfaccia utente|  
|System.Console.ReadKey()|Interfaccia utente|  
|System.Console.ReadLine()|Interfaccia utente|  
|System.Console.SetError()|Interfaccia utente|  
|System.Console.SetIn()|Interfaccia utente|  
|System.Console.SetOut()|Interfaccia utente|  
|System.Console.Write()|Interfaccia utente|  
|System.Console.WriteLine()|Interfaccia utente|  
|System.Diagnostics.LogMessageEventHandler|ExternalThreading, Synchronization|  
|System.IO.FileStream.BeginRead()|ExternalThreading|  
|System.IO.FileStream.BeginWrite()|ExternalThreading|  
|System.IO.Stream.Synchronized()|Sincronizzazione|  
|System.IO.TextReader.Synchronized()|Sincronizzazione|  
|System.IO.TextWriter.Synchronized()|Sincronizzazione|  
|System.Reflection.Emit.AssemblyBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.ConstructorBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.CustomAttributeBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.EnumBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.EventBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.FieldBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.MethodBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.MethodRental|MayLeakOnAbort|  
|System.Reflection.Emit.ModuleBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.PropertyBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.TypeBuilder|MayLeakOnAbort|  
|System.Reflection.Emit.UnmanagedMarshal|MayLeakOnAbort|  
|System.Security.Principal.WindowsPrincipal|SecurityInfrastructure|  
|System.Threading.AutoResetEvent|ExternalThreading, Synchronization|  
|System.Threading.EventWaitHandle|ExternalThreading, Synchronization|  
|System.Threading.ManualResetEvent|ExternalThreading, Synchronization|  
|System.Threading.Monitor|ExternalThreading, Synchronization|  
|System.Threading.Mutex|ExternalThreading, Synchronization|  
|System.Threading.ReaderWriterLock|ExternalThreading, Synchronization|  
|System.Threading.Thread.AllocateDataSlot()|ExternalThreading, SharedState|  
|System.Threading.Thread.AllocateNamedDataSlot()|ExternalThreading, SharedState|  
|System.Threading.Thread.BeginCriticalRegion()|ExternalThreading, Synchronization|  
|System.Threading.Thread.EndCriticalRegion()|ExternalThreading, Synchronization|  
|System.Threading.Thread.FreeNamedDataSlot()|ExternalThreading, SharedState|  
|System.Threading.Thread.GetData()|ExternalThreading, SharedState|  
|System.Threading.Thread.GetNamedDataSlot()|ExternalThreading, SharedState|  
|System.Threading.Thread.Join()|ExternalThreading, Synchronization|  
|System.Threading.Thread.set_ApartmentState()|Synchronization, SelfAffectingThreading|  
|System.Threading.Thread.set_CurrentUICulture()|ExternalThreading|  
|System.Threading.Thread.set_IsBackground()|SelfAffectingThreading|  
|System.Threading.Thread.set_Name()|ExternalThreading|  
|System.Threading.Thread.set_Priority()|SelfAffectingThreading|  
|System.Threading.Thread.SetApartmentState()|Synchronization, SelfAffectingThreading|  
|System.Threading.Thread.SetData()|ExternalThreading, SharedState|  
|System.Threading.Thread.SpinWait()|ExternalThreading, Synchronization|  
|System.Threading.Thread.Start()|ExternalThreading, Synchronization|  
|System.Threading.Thread.TrySetApartmentState()|Synchronization, SelfAffectingThreading|  
|System.Threading.ThreadPool|ExternalThreading, Synchronization|  
|System.Threading.Timer|ExternalThreading, Synchronization|  
|System.Threading.TimerBase|ExternalThreading, Synchronization|  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi di protezione host e programmazione dell'integrazione con CLR](host-protection-attributes-and-clr-integration-programming.md)   
 [Tipi e membri non consentiti in Microsoft.VisualBasic.dll](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipi e membri non consentiti in System.dll](disallowed-types-and-members-in-system-dll.md)   
 [Tipi e membri non consentiti in System.Data.dll](disallowed-types-and-members-in-system-data-dll.md)   
 [Tipi e membri non consentiti in System.Core.dll](disallowed-types-and-members-in-system-core-dll.md)  
  
  
