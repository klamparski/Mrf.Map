# Neos CMS Google Maps Plugin

Mrf.Map plugin adds easily customizable Google Map Node Type to your Neos CMS site.

## Installation

To install the package use composer require command in the CLI:

```
composer require mrf/map:1.*
```

Or just add it manually to your composer.json by adding following line in "require" section:

```
"mrf/map": "1.*"
```

Then install the composer packages by command in the CLI:

```
composer update
```

## Extending map options
 
Mrf.Map package makes it easy to extend Google Map settings. If you would like to hardcode new settings globally for whole site, you just need to add few lines of TypoScript in your site package (e.g. Resources/Private/TypoScript/Root.ts2):
 
```
prototype(Mrf.Map:GoogleMap) {
	jsVars {
    	mapOptions {
        	streetViewControl = ${String.toBoolean('0')}
		}
	}
}
 ```

You can also easily make new setting configurable from the Neos inspector. To do it, you just need to extend the node type definition in your site package (e.g. Configuration/NodeTypes.yaml):

```yaml
'Mrf.Map:GoogleMap':
  properties:
    streetViewControl:
      type: boolean
      defaultValue: TRUE
      ui:
        label: 'Allow street view control'
        inspector:
          group: 'settings'
```
 
 And use it in your site TypoScript (e.g. Resources/Private/TypoScript/Root.ts2)
 
```
prototype(Mrf.Map:GoogleMap) {
	jsVars {
		mapOptions {
			streetViewControl = ${String.toBoolean(q(node).property('streetViewControl'))}
		}
	}
}
```