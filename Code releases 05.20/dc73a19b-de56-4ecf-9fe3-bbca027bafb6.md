## Upgrading from Version 4.* to Version 5.*

Version 5 of the CMSGui module introduces the [multi-store functionality](https://documentation.spryker.com/docs/en/multi-store-cms-pages-201903). The multi-store CMS page feature enables management of CMS page display per store via a store toggle control in the Back Office.

@(Error)()(To enable the feature, make sure you have the store relation type plugin. See below for details.)

**To upgrade to the new version of the module, do the following:**

1. Require the update with composer: `"spryker/cms-gui": "^5.0.0"`
2. Add the Store Relation Form Type Plugin:

src/Pyz/Zed/CmsGui/CmsGuiDependencyProvider.php

```php
use Spryker\Zed\Kernel\Communication\Form\FormTypeInterface;
use Spryker\Zed\Store\Communication\Plugin\Form\StoreRelationToggleFormTypePlugin;

class CmsGuiDependencyProvider extends SprykerCmsGuiDependencyProvider
{
	/**
	* @return \Spryker\Zed\Kernel\Communication\Form\FormTypeInterface
	*/
	protected function getStoreRelationFormTypePlugin(): FormTypeInterface
	{
		return new StoreRelationToggleFormTypePlugin();
	}
}
```
    
New transfers must be generated:
`$ console transfer:generate`

3. If project overrides were introduced, please observe the following changes:
* `CmsGuiCommunicationFactory::createCmsVersionForm` was deprecated, please use `CmsGuiCommunicationFactory::getCmsVersionForm`.
* `CmsGuiCommunicationFactory::createCmsGlossaryForm` was deprecated, please use `CmsGuiCommunicationFactory::getCmsGlossaryForm`.
* `CmsVersionMapper::mapToCmsVersionDataTransfer` was given return type `CmsVersionMapper::CmsVersionDataTransfer`

_Estimated migration time: 30 minutes._