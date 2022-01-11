---
layout: post
title:  "Azure AD Domain Verification"
date:   2016-12-12 15:48:37 -0500
categories: Azure update
author: joseph
---
Azure AD Domain Verification
====

2016-12-12 15:24:27
            
---


**Setup domain verification**
Microsoft wants a @ in the txt record.
However, the @ sign just means the dns origin is the same for the domain.
So if the msoft request is
@.familyhosted.com

And @ isn't allowed with your registrar and you are trying to authorize internal.familyhosted.com you can just replace the @ with "internal"

The @ is more of a wildcard meant to make the process easer and doesn't require more work on msofts side.
Internal.familyhosted.com

**Windows
**Check GPOs and ensure WMI has trust groups with right ip subnets as trusted hosts


**Enable remote disk mgmt**
```powershell
Enable-Netfirewall
Sc start vds
```







