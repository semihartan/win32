---
title: Example Adding a Helper Token to a BITS Transfer Job
description: You can configure a Background Intelligent Transfer Service (BITS) transfer job with an additional security token. The BITS transfer job uses this helper token for authentication and to access resources.
ms.assetid: '08670c6d-e589-41be-842d-597f460d9c97'
---

# Example: Adding a Helper Token to a BITS Transfer Job

You can configure a Background Intelligent Transfer Service (BITS) transfer job with an additional security token. The BITS transfer job uses this helper token for authentication and to access resources.

For more information, see [Helper tokens for BITS transfer jobs](helper-tokens-for-bits-transfer-jobs.md).

The following procedure creates a BITS transfer job in the context of the local user, gets credentials of a second user, creates a helper token with these credentials, and then sets the helper token on the BITS transfer job.

This example uses the header and implementation defined in [Example: Common Classes](common-classes.md).

**To add a helper token to a BITS transfer job**

1.  Initialize COM parameters by calling the CCoInitializer function. For more information about the CCoInitializer function, see [Example: Common Classes](common-classes.md).
2.  Get a pointer to the [**IBackgroundCopyJob**](ibackgroundcopyjob.md) interface. This example uses the [CComPtr Class](http://go.microsoft.com/fwlink/p/?linkid=162393) to manage COM interface pointers.
3.  Initialize COM process security by calling [CoInitializeSecurity](http://go.microsoft.com/fwlink/p/?linkid=162390). BITS requires at least the IMPERSONATE level of impersonation. BITS fails with E\_ACCESSDENIED if the correct impersonation level is not set.
4.  Get a pointer to the [**IBackgroundCopyManager**](ibackgroundcopymanager.md) interface, and obtain the initial locator to BITS by calling the [CoCreateInstance]( http://go.microsoft.com/fwlink/p/?linkid=162386) function.
5.  Create a BITS transfer job by calling the [**IBackgroundCopyManager::CreateJob**](ibackgroundcopymanager-createjob.md) method.
6.  Get a pointer to the CNotifyInterface callback interface, and call the [**IBackgroundCopyJob::SetNotifyInterface**](ibackgroundcopyjob-setnotifyinterface.md) method to receive notification of job-related events. For more information about CNotifyInterface, see [Example: Common Classes](common-classes.md).
7.  Call the [**IBackgroundCopyJob::SetNotifyFlags**](ibackgroundcopyjob-setnotifyflags.md) method to set the types of notifications to receive. In this example, the **BG\_NOTIFY\_JOB\_TRANSFERRED** and **BG\_NOTIFY\_JOB\_ERROR** flags are set.
8.  Get a pointer to the [**IBitsTokenOptions**](ibitstokenoptions.md) interface by calling the **IBackgroundCopyJob::QueryInterface** method with the proper interface identifier.
9.  Attempt to log on the user of the helper token. Create an impersonation handle, and call the [LogonUser Function]( http://go.microsoft.com/fwlink/p/?linkid=162396) to populate the impersonation handle. If successful, call the [ImpersonateLoggedOnUser Function](http://go.microsoft.com/fwlink/p/?linkid=162395). If unsuccessful, the example calls the [RevertToSelf Function](http://go.microsoft.com/fwlink/p/?linkid=162397) to terminate the impersonation of the logged-on user, an error is thrown, and the handle is closed.
10. Call the [**IBitsTokenOptions::SetHelperToken**](ibitstokenoptions-sethelpertoken.md) method to impersonate the token of the logged-on user. If this method fails, the example calls the [RevertToSelf Function](http://go.microsoft.com/fwlink/p/?linkid=162397) to terminate the impersonation of the logged-on user, an error is thrown, and the handle is closed.
    > [!Note]
    >
    > In supported versions of Windows before Windows 10, version 1607, the job owner must have administrative credentials to call the [**IBitsTokenOptions::SetHelperToken**](ibitstokenoptions-sethelpertoken.md) method.
    >
    > Starting with Windows 10, version 1607, non-administrator job owners can set non-administrator helper tokens on BITS jobs they own. Job owners must still have administrative credentials to set helper tokens with administrator privileges.

     

11. Call the [**IBitsTokenOptions::SetHelperTokenFlags**](ibitstokenoptions-sethelpertokenflags.md) method to specify which resources to access using the helper token's security context.
12. After the impersonation is complete, the example calls the [RevertToSelf Function](http://go.microsoft.com/fwlink/p/?linkid=162397) to terminate the impersonation of logged on user, and the handle is closed.
13. Add files to the BITS transfer job by calling [**IBackgroundCopyJob::AddFile**](ibackgroundcopyjob-addfile.md).
14. After the file is added, call [**IBackgroundCopyJob::Resume**](ibackgroundcopyjob-resume.md) to resume the job.
15. Set up a while loop to wait for the quit message from the callback interface while the job is transferring. The while loop uses the [GetTickCount](http://go.microsoft.com/fwlink/p/?linkid=162392) function to retrieve the number of milliseconds that have elapsed since the job started transferring.
16. After the BITS transfer job is complete, remove the job from the queue by calling [**IBackgroundCopyJob::Complete**](ibackgroundcopyjob-complete.md).

The following code example adds a helper token to a BITS transfer job.


```C++
#include <bits.h>
#include <bits4_0.h>
#include <stdio.h>
#include <tchar.h>
#include <lm.h>
#include <iostream>
#include <exception>
#include <string>
#include <atlbase.h>
#include <memory>
#include <new>
#include "CommonCode.h"


void HelperToken(const LPWSTR &amp;remoteFile, const LPWSTR &amp;localFile, const LPWSTR &amp;domain, const LPWSTR &amp;username, const LPWSTR &amp;password)
{
// If CoInitializeEx fails, the exception is unhandled and the program terminates   
CCoInitializer coInitializer(COINIT_APARTMENTTHREADED);

CComPtr<IBackgroundCopyJob> pJob; 

    try
    {
        //The impersonation level must be at least RPC_C_IMP_LEVEL_IMPERSONATE.
        HRESULT hr = CoInitializeSecurity(
            NULL,
            -1,
            NULL,
            NULL,
            RPC_C_AUTHN_LEVEL_CONNECT,
            RPC_C_IMP_LEVEL_IMPERSONATE,
            NULL,
            EOAC_DYNAMIC_CLOAKING,
            0
            );

        if (FAILED(hr))
        {
            throw MyException(hr, L"CoInitializeSecurity");
        }

        // Connect to BITS.
        CComPtr<IBackgroundCopyManager> pQueueMgr;
        hr = CoCreateInstance(__uuidof(BackgroundCopyManager), NULL,
            CLSCTX_LOCAL_SERVER,
            __uuidof(IBackgroundCopyManager),
            (void **)&amp;pQueueMgr);

        if (FAILED(hr))
        {
            // Failed to connect.
            throw MyException(hr, L"CoCreateInstance");
        }

        // Create a job.
        wprintf(L"Creating Job...\n");

        GUID guidJob;
        hr = pQueueMgr->CreateJob(L"HelperTokenSample",
            BG_JOB_TYPE_DOWNLOAD,
            &amp;guidJob,
            &amp;pJob);


        if(FAILED(hr))
        {   
            // Failed to create job.
            throw MyException(hr, L"CreateJob");
        }

        // Set the File Completed call.
        CComPtr<CNotifyInterface> pNotify;    
        pNotify = new CNotifyInterface();
        hr = pJob->SetNotifyInterface(pNotify);
        if (FAILED(hr))
        {
            // Failed to SetNotifyInterface.
            throw MyException(hr, L"SetNotifyInterface");
        }
        hr = pJob->SetNotifyFlags(BG_NOTIFY_JOB_TRANSFERRED | 
            BG_NOTIFY_JOB_ERROR);

        if (FAILED(hr))
        {
            // Failed to SetNotifyFlags.
            throw MyException(hr, L"SetNotifyFlags");
        }

        //Retrieve the IBitsTokenOptions interface pointer from the BITS transfer job.
        CComPtr<IBitsTokenOptions> pTokenOptions;
        hr = pJob->QueryInterface(__uuidof(IBitsTokenOptions), (void** ) &amp;pTokenOptions);

        if (FAILED(hr))
        {
            // Failed to QueryInterface.
            throw MyException(hr, L"QueryInterface");
        }

        // Log on user of the helper token.
        wprintf(L"Credentials for helper token %s\\%s %s\n", domain, username, password);

        HANDLE hImpersonation = INVALID_HANDLE_VALUE;
        if(LogonUser(username, domain, password, LOGON32_LOGON_INTERACTIVE, LOGON32_PROVIDER_DEFAULT, &amp;hImpersonation))
        {
            // Impersonate the logged-on user.
            if(ImpersonateLoggedOnUser(hImpersonation))
            {
                // Configure the impersonated logged-on user's token as the helper token.
                hr = pTokenOptions->SetHelperToken();        
                if (FAILED(hr))
                {
                    //Failed to set helper token.
                    CloseHandle(hImpersonation);
                    RevertToSelf();
                    throw MyException(hr, L"SetHelperToken");
                }

                hr = pTokenOptions->SetHelperTokenFlags(BG_TOKEN_LOCAL_FILE);
                if (FAILED(hr))
                {
                    //Failed to set helper token flags.
                    CloseHandle(hImpersonation);
                    RevertToSelf();
                    throw MyException(hr, L"SetHelperTokenFlags");
                }

                RevertToSelf();
            }               
            CloseHandle(hImpersonation);
        }

        // Add a file.
        // Replace parameters with variables that contain valid paths.
        wprintf(L"Adding File to Job\n");
        hr = pJob->AddFile(remoteFile,localFile);

        if(FAILED(hr))
        {   
            //Failed to add file to job.
            throw MyException(hr, L"AddFile");
        }

        //Resume the job.
        wprintf(L"Resuming Job...\n");
        hr = pJob->Resume();
        if (FAILED(hr))
        {
            // Resume failed.                   
            throw MyException(hr, L"Resume");
        }    
    }
    catch(const std::bad_alloc &amp;)
    {
        wprintf(L"Memory allocation failed");
        if (pJob)
        {
            pJob->Cancel();
        }

        return;
    }
    catch(const MyException &amp;ex)
    {
        wprintf(L"Error 0x%x occurred during operation", ex.Error);
        if (pJob)
        {
            pJob->Cancel();
        }

        return;
    }

    wprintf(L"Transferring file and waiting for callback.\n");

    // Wait for QuitMessage from CallBack
    DWORD dwLimit = GetTickCount() + (15 * 60 * 1000);  // set 15 minute limit
    while (dwLimit > GetTickCount())
    {
        MSG msg;

        while (PeekMessage(&amp;msg, NULL, 0, 0, PM_REMOVE)) 
        { 
            // If it is a quit message, exit.
            if (msg.message == WM_QUIT) 
            {
                return;
            }

            // Otherwise, dispatch the message.
            DispatchMessage(&amp;msg); 
        } // End of PeekMessage while loop
    }

    pJob->Cancel();
    return;
}

void _cdecl _tmain(int argc, LPWSTR* argv)
{   
    if (argc != 6)
    {
        wprintf(L"Usage:");
        wprintf(L"%s ", argv[0]);
        wprintf(L"[remote name] [local name] [helpertoken domain] [helpertoken userrname] [helpertoken password]\n");
        return;
    }

    HelperToken(argv[1],argv[2],argv[3],argv[4],argv[5]);

}
```



## Related topics

<dl> <dt>

[Helper tokens for BITS transfer jobs](helper-tokens-for-bits-transfer-jobs.md)
</dt> <dt>

[**IBitsTokenOptions**](ibitstokenoptions.md)
</dt> <dt>

[Example: Common Classes](common-classes.md)
</dt> </dl>

 

 



