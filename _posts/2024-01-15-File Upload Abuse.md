---
layout: post
title: "File Upload Exploitation"
subtitle: "Abuse of Public File Upload Features"
background: '/img/posts/Malware.jpg'
---

## Background
Web applications frequently enable users to upload files for various purposes such as profile photos, avatars, photo sharing, animated GIFs in forums, layout customization, and file distribution (PDF, Word, Excel). However, potential abuses arise when users upload too many files, files that are excessively large, or files at a high frequency. Such actions can strain a system's file storage resources, causing depletion. Additionally, users may inadvertently or intentionally upload files with the wrong content type, creating mismatches with the application's expectations (e.g., uploading a movie instead of an image). These abuses, whether accidental or intentional, pose risks such as server slowdowns, connection monopolization, and potential denial of service.


![IMDb page](/img/posts/Carnabotnet.jpg)

## Malware
The most severe form of file upload abuse involves the uploading of malware, a term derived from "malicious software." When a file containing malware is accessed, the malware is triggered. To avoid detection, malware may disguise itself as a different file type and even be embedded within seemingly harmless formats such as images, PDFs, or other media assets.

#### Malware encompasses various types, each serving different purposes and pursuing distinct goals:

1. Adware
2. Bots and botnets
3. Spam
4. Denial of Service (DoS)
5. Ransomware
6. Spyware
7. Keystroke loggers
8. Data harvesting
9. Webcam activation
10. Bypassing access controls
11. Rootkit (total server control)

These diverse forms of malware pose significant threats, ranging from unwanted advertisements and system manipulation to data breaches and complete control over servers.
