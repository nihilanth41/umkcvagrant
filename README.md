# umkcvagrant

## Introduction
This module facilitates development in the Islandora Vagrant environment by creating Fedora repository object(s) using the Islandora Tuque wrapper.   

More specifically, it uses the IslandoraTuque wrapper to create the Root Collection PID for each of the following islandora sites: 

* MU (mu:root)
* UMKC (umkc:root)
* UMKC Law (umkclaw:root)
* UMKC Scholar (umkcscholar:root)
* UMSL 
	- (islandora:336)
	- (umsl:root)

## Requirements

This module requires the following modules/libraries: 

* [Islandora](https://github.com/islandora/islandora)

## Installation

To install, enable the module with drush as follows:   
``` 
cd /var/www/drupal/sites/all/modules
git clone https://github.com/nihilanth41/umkcvagrant.git
drush -y -u 1 en umkcvagrant
```

To uninstall, just disable the module with drush.    
The module will attempt to delete all of the root collection PIDs that were created.
```
cd /var/www/drupal/sites/all/modules
drush -y -u 1 dis umkcvagrant
```

## Configuration

Each site has slightly different datastreams (E.g., not every collection has a mods.xml) so the files that need to be ingested are specified explicitly for each site.   

The datastreams for an existing collection can be found in Drupal at: 
`http://{sitename}/islandora/object/{pid}/manage/datastreams`   
or through the Fedora API-A at:   
`http://{sitename}:8080/fedora/objects/{pid}/datastreams`

To add another collection: 
* download the datastream files into `{module_path}/datastreams/{sitename}/`   
* modify (append) the .module file with steps to ingest all of the datastreams. 
	- The other sites can be used as a template/example.

### Note about UMSL site

The root collection for the UMSL site (umsl:root) is in it's own namespace (umsl) restricted from the other sites.  
It's also a sub-collection of a collection (islandora:336) in the default namespace (islandora).   
For this reason, the collection in the default namespace is created first (Called UMSL Test Collection), then the actual UMSL root collection is created as a sub-collection of that.  
Since the namespace is restricted the umsl:root collection is only viewable in islandora under the UMSL site. 

## Links

https://github.com/Islandora/islandora/wiki/Working-With-Fedora-Objects-Programmatically-Via-Tuque

