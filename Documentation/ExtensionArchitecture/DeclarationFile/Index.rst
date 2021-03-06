.. include:: ../../Includes.txt


.. _extension-declaration:


=================================
Declaration File (ext_emconf.php)
=================================

*-- required*

The :file:`ext_emconf.php` is the single most important file in an extension.
Without it, the Extension Manager (EM) will not detect the extension, much less
be able to install it. This file contains a declaration of what the extension
is or does for the EM. The only thing included
is an associative array, :code:`$EM_CONF[extension key]`.
The keys are described in the table below.

This file is overwritten, when extensions are imported from the online repository. So don't write your custom code in this file - only change
values in the :code:`$EM_CONF` array if needed.

.. t3-field-list-table::
 :header-rows: 1

 - :Key,20: Key
   :Data type,20: Data type
   :Description,60: Description

 - :Key:
         title
   :Data type:
         string, required
   :Description:
         The name of the extension in English.

 - :Key:
         description
   :Data type:
         string, required
   :Description:
         Short and precise description in English of what the extension does
         and for whom it might be useful.

 - :Key:
         version
   :Data type:
         string
   :Description:
         Version of the extension. Automatically managed by EM / TER. Format is
         [int].[int].[int]
 - :Key:
         category
   :Data type:
         string
   :Description:
         Which category the extension belongs to:

         - **be**

           Backend (Generally backend-oriented, but not a module)

         - **module**

           Backend modules (When something is a module or connects with one)

         - **fe**

           Frontend (Generally frontend oriented, but not a "true" plugin)

         - **plugin**

           Frontend plugins (Plugins inserted as a "Insert Plugin" content
           element)

         - **misc**

           Miscellaneous stuff (Where not easily placed elsewhere)

         - **services**

           Contains TYPO3 services

         - **templates**

           Contains website templates

         - **example**

           Example extension (Which serves as examples etc.)

         - **doc**

           Documentation (e.g. tutorials, FAQ's etc.)

         - **distribution**

           Distribution, an extension kickstarting a full site

 - :Key:
         constraints
   :Data type:
         array
   :Description:
         List of requirements, suggestions or conflicts with other extensions
         or TYPO3 or PHP version. Here's how a typical setup might look::

            'constraints' => array(
                'depends' => array(
                    'typo3' => '4.5.0-6.1.99',
                    'php' => '5.3.0-5.5.99'
                ),
                'conflicts' => array(
                    'dam' => ''
                ),
                'suggests' => array(
                    'tt_news' => '2.5.0-0.0.0'
                )
            )

         depends
           List of extensions that this extension depends on.
           Extensions defined here will be loaded *before* the current extension.

         conflicts
            List of extensions which will not work with this extension.

         suggests
           List of suggestions of extensions that work together or
           enhance this extension.
           Extensions defined here will be loaded *before* the current extension.
           Dependencies take precedence over suggestions.

           **Note:** If a "suggested" extension depends on the current extension
           (directly or indirectly), the suggestion is not
           taken into account for loading order calculation.
           Read more at :forge:`57825`.

         The above example indicated that the extension depends on a
         version of TYPO3 between 4.5 and 6.1 (as only bug and security fixes are
         integrated into TYPO3 when the last digit of the version changes, it is
         safe to assume it will be compatible with any upcoming version of the
         corresponding branch, thus ``.99``). Also the extension has been
         tested and is known to work properly with PHP 5.3, 5.4 and 5.5. It
         will conflict with the DAM (any version) and it is suggested that it
         might be worth installing "tt\_news" (version at least 2.5.0).

 - :Key:
         state
   :Data type:
         string
   :Description:
         Which state is the extension in

         - **alpha**

           Alpha state is used for very initial work, basically the state is has
           during the very process of creating its foundation.

         - **beta**

           Under current development. Beta extensions are functional but not
           complete in functionality. Most likely beta-extensions will not be
           reviewed.

         - **stable**

           Stable extensions are complete, mature and ready for production
           environment. You will be approached for a review. Authors of stable
           extensions carry a responsibility to maintain and improve them.

         - **experimental**

           Experimental state is useful for anything experimental - of course.
           Nobody knows if this is going anywhere yet... Maybe still just an
           idea.

         - **test**

           Test extension, demonstrates concepts, etc.

         - **obsolete**

           The extension is obsolete or deprecated. This can be due to other
           extensions solving the same problem but in a better way or if the
           extension is not being maintained anymore.

         - **excludeFromUpdates**

           This state makes it impossible to update the
           extension through the Extension Manager (neither by the Update
           mechanism, nor by uploading a newer version to the installation). This
           is very useful if you made local changes to an extension for a
           specific installation and don't want any admin to overwrite them.

           *New since TYPO3 4.3.*

 - :Key:
         uploadfolder
   :Data type:
         boolean
   :Description:
         If set, then the folder named "uploads/tx\_[extKey-with-no-
         underscore]" should be present!

 - :Key:
         createDirs
   :Data type:
         list of strings
   :Description:
         Comma list of directories to create upon extension installation.

 - :Key:
         clearCacheOnLoad
   :Data type:
         boolean
   :Description:
         If set, the EM will request the cache to be cleared when this
         extension is loaded.

 - :Key:
         author
   :Data type:
         string
   :Description:
         Author name

 - :Key:
         author\_email
   :Data type:
         email address
   :Description:
         Author email address

 - :Key:
         author\_company
   :Data type:
         string
   :Description:
         Author company


 - :Key:
         autoload
   :Data type:
         array
   :Description:
         To get better class loading support for websites in **non-composer mode+** 
         the following information can be provided.
         
         **Extensions having one folder with classes or single files**
         
         Considering you have an Extbase extension (or an extension where all classes 
         and interfaces reside in a :file:`Classes` folder) or single classes you can simply
         add the following to your :file:`ext_emconf.php` file::

            'autoload' => [
               'classmap' => [
                  'Classes',
                  'a-class.php',
               ]
            ],
            
         **Extensions using namespaces**
         
         If the extension has namespaced classes following the PSR-4 standard, then you 
         can add the following to your :file:`ext_emconf.php` file::
         
            'autoload' => [
               'psr-4' => [
                  'Vendor\\ExtName\\' => 'Classes'
               ]
            ],
            
         // Important: The prefix must end with a backslash.          

 - :Key:
         autoload-dev
   :Data type:
         array
   :Description:
         Same as the configuration "autoload" but it is only used if the 
         *ApplicationContext* is set to *Testing*.
  

Deprecated Configuration
========================

The following fields are deprecated and should not be used anymore:

- dependencies
- conflicts
- suggests 
- docPath 
- CGLcompliance
- CGLcompliance_note
- private
- download_password
- shy
- loadOrder
- priority
- internal
- modify_tables
- module
- lockType
- TYPO3_version
- PHP_version
