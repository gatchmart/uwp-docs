---
title: Resolving Telerik named resources
page_title: Resolving Telerik named resources
description: Resolving Telerik named resources
slug: common-resolvingteleriknamedresources
tags: resolving,telerik,named,resources
published: False
position: 1
---

# Resolving Telerik named resources

Before customizing the default control template of any **Telerik Controls** what you need to know is that each default control template contains references to predefined Telerik resources. Due to the specific way of styling these resources are loaded dynamically in the application resources.     

To refer the predefined Telerik named resources in **Windows 8.1 / Windows Phone 8.1 and UWP** you have to add the resource dictionaries that contain these resources in your **Application.Resources** (in the **App.xaml** file). For each theme you would like to support, you have to add a **ResourceDictionary** with the corresponding theme key. In this dictionary you have to merge all dictionaries where the needed resources are defined in order to freely refer them in your project.

	<ResourceDictionary>
		<ResourceDictionary.ThemeDictionaries>
			<ResourceDictionary x:Key="Default">
				<ResourceDictionary.MergedDictionaries>
					<ResourceDictionary Source="ms-appx:///ControlAssembly/Themes/ThemeResourcesDark.xaml"/>
					<ResourceDictionary Source="ms-appx:///OtherControlAssemmbly/Themes/ThemeResourcesDark.xaml"/>
				</ResourceDictionary.MergedDictionaries>
			</ResourceDictionary>
			<ResourceDictionary x:Key="Light">
				<ResourceDictionary.MergedDictionaries>
					<ResourceDictionary Source="ms-appx:///ControlAssembly/Themes/ThemeResourcesLight.xaml"/>
					<ResourceDictionary Source="ms-appx:///OtherControlAssembly/Themes/ThemeResourcesLight.xaml"/>
				</ResourceDictionary.MergedDictionaries>
			</ResourceDictionary>
		</ResourceDictionary.ThemeDictionaries>
	</ResourceDictionary>

Where *ControlNamespace* is the specific namespace where the control you restyle is defined.

|UI component|WinRT namespace|UWP namespace|
|:-|:-|:-|
|RadChart|Telerik.UI.Xaml.Chart|Telerik.UI.Xaml.Chart.UWP|
|RadGrid|Telerik.UI.Xaml.Grid|Telerik.UI.Xaml.Grid.UWP|
|RadDatePicker, RadTimePicker, RadAutoCompleteBox, RadNumericBox, RadRangeSlider|Telerik.UI.Xaml.Input|Telerik.UI.Xaml.Input.UWP|
|RadHubTile, RadLegendControl, RadRadialMenu|Telerik.UI.Xaml.Primitives|Telerik.UI.Xaml.Primitives.UWP|
|RadGauge, RadBulletGraph|Telerik.UI.Xaml.DataVisualization|Telerik.UI.Xaml.DataVisualization.UWP|

If you wish to override some of the Telerik named resources (e.g. to change the color of a Telerik named brush), you have to use the mechanism described in the [Telerik Named Brushes]({%slug common-teleriknamedbrushes%}) article and you will need to merge the following **ResourceDictionary** in the **Application.Resources**:

	<ResourceDictionary>
		<telerik:UserThemeResources x:Key="ThemeResource" DarkResourcesPath="ms-appx:///Dark.xaml" LightResourcesPath="ms-appx:///Light.xaml"/>
		<ResourceDictionary.ThemeDictionaries>
			<ResourceDictionary x:Key="Default">
				<ResourceDictionary.MergedDictionaries>
					<ResourceDictionary Source="ms-appx:///ControlAssembly/Themes/ThemeResourcesDark.xaml"/>
					<ResourceDictionary Source="ms-appx:///OtherControlAssembly/Themes/ThemeResourcesDark.xaml"/>
					<ResourceDictionary Source="{CustomResource DarkResourcesPath}"/>
				</ResourceDictionary.MergedDictionaries>
			</ResourceDictionary>
			<ResourceDictionary x:Key="Light">
				<ResourceDictionary.MergedDictionaries>
					<ResourceDictionary Source="ms-appx:///ControlAssembly/Themes/ThemeResourcesLight.xaml"/>
					<ResourceDictionary Source="ms-appx:///OtherControlAssembly/Themes/ThemeResourcesLight.xaml"/>
					<ResourceDictionary Source="{CustomResource LightResourcesPath}"/>
				</ResourceDictionary.MergedDictionaries>
			</ResourceDictionary>
		</ResourceDictionary.ThemeDictionaries>
	</ResourceDictionary>

Where:

	xmlns:telerik="using:Telerik.UI.Xaml.Controls"

# See Also

 * [Telerik Named Brushes]({%slug common-teleriknamedbrushes%})