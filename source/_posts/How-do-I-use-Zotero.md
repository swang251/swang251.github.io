---
title: How do I use Zotero?
mathjax: true
toc: true
date: 2020-01-07 10:30:24
tags: [Zotero, Org-mode, Emacs]
categories: Research Daily
---

I used Endnote as my first reference management software when I started my master study. I also tried a little bit Mendeley and saw how well it is intrinsically coupled Elsevier publications and the PDF editor. However, I finally decided to use [Zotero](https://www.zotero.org/) mainly because it is an open-source software and is more flexible. 

<!--more-->
## Workflow
- Read the [documentation](https://www.zotero.org/support/start)
- [Adding Items to Zotero](https://www.zotero.org/support/adding_items_to_zotero)
  - We need to install the *Zotero Connector* for Chrome, Firefox, or other web browsers.
  - We need to launch the Zotero desktop application before he could save items to Zotero.
- [Adding files to items](https://www.zotero.org/support/attaching_files#adding_files)
  - the *Zotero Connector* provides an automatic routine to save the PDF to the Zotero. 
  - However, I personally prefer to "manually" save the PDFs using [ZotFile](#zotfile).
- Organize your PDFs: see [below](#pdf-organization)
- Adding notes to items: here I list two options
  - [Markdown](https://daringfireball.net/projects/markdown/syntax): use [*Markdown Here*](#markdown-here)
  - [Org mode](https://orgmode.org/): use [*.org*](#org-mode) attachments

## Attachements/PDFs Organization
There are two options here to manage your attachments: [stored files and linked files](https://www.zotero.org/support/attaching_files#stored_files_and_linked_files).

### Save and sync the attachements in your Zotero library
- All your attachments will be stored in `${Zotero}\storage` (set your Data Directory Location in `preference`-`Advanced`-`Files and Folders`), since everything is coded and automatically organized, you will see a series of folders likely named as `2NEHBKP9`.
- Zotero allows you to sync your files/attachements in My Library. All the attachements you put under the items can be synchronized to the [Zotero Storage](https://www.zotero.org/storage) or your own WebDAV. 
   - You can modify it by going to the `preference` $\rightarrow$ `Sync` $\rightarrow$ `Settings` $\rightarrow$ `File Syncing`
   - Check/uncheck the `Sync attachement files in My Library using` 
   - Select `Zotero` or `WebDAV`.
   - If you select `WebDAV`, you will need to provide your account infomation.
     - Here is how it works using [Jianguoyun](https://www.jianguoyun.com): [坚果云第三方应用授权WebDAV开启方法](http://help.jianguoyun.com/?p=2064)


**However, there are two limitation of the this method:**

- Zotero storage is not free
- The cloud storage you are using, like [Dropbox, doesn't support WebDAV](https://help.dropbox.com/installs-integrations/third-party/webdav-or-ftp)

So here is another way to organize and sync your attachements.

### Save the links to the PDFs in your Zotero library. 
Zotero allows you to store the link to files in My Library.

- Set the set your [base directory](https://www.zotero.org/support/preferences/advanced#linked_attachment_base_directory) by going to the `Preference` $\rightarrow$ `Advanced` $\rightarrow$ `Files and Folders` $\rightarrow$ `Linked Attachment Base Directory`. This way, links are stored as the relative path in your library so that is easier when you access the linked files on different computers.
- Use ZotFile for a linked-file workflow
  
### ZotFile
> [ZotFile](http://zotfile.com/) is a Zotero plugin to manage your attachments: automatically rename, move, and attach PDFs (or other files) to Zotero items, sync PDFs from your Zotero library to your (mobile) PDF reader (e.g. an iPad, Android tablet, etc.) and extract annotations from PDF files.

- ZotFile Preferences $\rightarrow$ Renaming Rules 
- ZotFile Preferences $\rightarrow$ General Setting
  - Source Folder for Attaching New Files: makes it easier to attach newly downloaded files. 
    - Download PDF $\rightarrow$ select the paper item $\rightarrow$ right click: Attach New File (ZotFile)
  - Location of Files
    - Attach stored copy of file(s)
	- Custom Location: 
	  - Use subfolder defined by `/%F`



## Note Management
### Markdown Here
> [Markdown Here](https://markdown-here.com/) is an extension for Chrome, Firefox, Safari, Opera, Thunderbird, and Postbox.

- One can [build the extension bundle](https://github.com/jlegewie/markdown-here#building-the-extension-bundles) from the source code and generate the `.xpi` file for Zotero
- Then in Zotero, go to Tools $\rightarrow$ Add-on $\rightarrow$ Install Add-on From File...
- When you edit the note, go to File $\rightarrow$ Markdown Toggle or use the hotkey `Ctrl+Alt+M` to switch back and forth between the plain and the rendered text

### Org-mode
> [Org mode](https://orgmode.org/) is for keeping notes, maintaining TODO lists, planning projects, and authoring documents with a fast and effective plain-text system.

I started to use Org mode in 2018 and gradually fall in love with it. To me, there is no substitute of Org mode. I tried different markdown softwares like Quiver, Joplin, etc. They are good, (especially the Joplin) but they cannot replace Org mode. Everything is foldable in Org mode which makes it much easier to explore and organize the documents. Also, considering how painful it is to keep notes in the Zotero-note, even with the [Markdown Here](https://markdown-here.com/), I decided to find a way out to use Org mode for writing reading summaries and notes which can be integrated with Zotero.

- create a `noteTemplate.org`
- Everytime you will add the note by 
  - Right click on items $\rightarrow$ Add Attachment $\rightarrow$ Attach Stored Copy of File $\rightarrow$ Select the `noteTemplate.org` 
  - Right click on `.org` file under the item $\rightarrow$ Rename File from Parent Metadata


### Zotxt
> [zotxt-emacs](https://gitlab.com/egh/zotxt-emacs) works with zotxt to provide an Emacs integration with Zotero, allowing you to manage citation keys for pandoc markdown documents as well as org mode links to items in your Zotero collection.
- Check [this article](http://www.mkbehr.com/posts/a-research-workflow-with-zotero-and-org-mode/) about using Zotxt

## Other 
### Better BibTeX for Zotero
> [Beter BibTex (BBT)](https://retorque.re/zotero-better-bibtex/) is an extension for Zotero and Juris-M that makes it easier to manage bibliographic data, especially for people authoring documents using text-based toolchains (e.g. based on LaTeX / Markdown).
- Automatically exports the `.bib` file and organizes the citation key.




