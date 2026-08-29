# Fortune Plugin

***Abandonment Notice:** I'm afraid I simply don't have the time to maintain my Grav themes and plugins. Those interested in taking over should refer to the ["Abandoned Resource Protocol"](https://learn.getgrav.org/17/advanced/grav-development#abandoned-resource-protoc). Feel free to fork and replace. So long, and thanks for all the fish.*

The **Fortune** Plugin is an extension for [Grav CMS](https://github.com/getgrav/grav). It will select a random quote from a folder containing [traditional "fortune" files](https://en.wikipedia.org/wiki/Fortune_(Unix)). There's [a demo](https://www.perlkonig.com/demos/fortune) on my personal website.

## Installation

Installing the Fortune plugin can be done in one of three ways: The GPM (Grav Package Manager) installation method lets you quickly install the plugin with a simple terminal command, the admin method lets you do so via the Admin Plugin, and the manual method lets you do so via a zip file.

### GPM Installation (Preferred)

To install the plugin via the [GPM](https://learn.getgrav.org/cli-console/grav-cli-gpm), through your system's terminal (also called the command line), navigate to the root of your Grav-installation, and enter:

    bin/gpm install fortune

This will install the Fortune plugin into your `/user/plugins`-directory within Grav. Its files can be found under `/your/site/grav/user/plugins/fortune`.

### Admin Plugin

If you use the Admin Plugin, you can install the plugin directly by browsing the `Plugins`-menu and clicking on the `Add` button.

### Manual Installation

To install the plugin manually, download the zip-version of this repository and unzip it under `/your/site/grav/user/plugins`. Then rename the folder to `fortune`. You can find these files on [GitHub](https://github.com/dharmann/grav-plugin-fortune) or via [GetGrav.org](https://getgrav.org/downloads/plugins).

You should now have all the plugin files under

    /your/site/grav/user/plugins/fortune
	
> NOTE: This plugin is a modular component for Grav which may require other plugins to operate, please see its [blueprints.yaml-file on GitHub](https://github.com/dharmann/grav-plugin-fortune/blob/main/blueprints.yaml).

## Configuration

If you use the Admin Plugin, a file with your configuration named fortune.yaml will be automatically created and saved in the `user/config/plugins/`-folder once the configuration is saved in the Admin.

**For those who do not use the Admin Plugin**, before configuring this plugin, you should copy the `user/plugins/fortune/fortune.yaml` to `user/config/plugins/fortune.yaml` and only edit that copy.

Here is the default configuration and an explanation of available options:

```yaml
enabled: true
data: 'user://data/fortunes'
```

Note that if you use the admin plugin, a file with your configuration, and named fortune.yaml will be saved in the `user/config/plugins/` folder once the configuration is saved in the admin.

* `enabled`: If set to false, the plugin will be disabled and won't execute.
* `data`: This is a *folder* containing as many fortune files as you want. By default it assumes you will create a `fortunes` folder under your `user/data` folder. But you can point elsewhere if you wish.

## Usage

### Adding & Indexing Fortunes

Fortune files are actually two files:

* The first is a plain text file (often without an extension) that contains multi-line quotes separated by lines containing only a percent symbol (`%`).

  ```
  Angels are very good at math. That's why they call them arc-angels.
    -- Steven Novella (The Skeptics Guide to the Universe)
  %
  There is no material safety data sheet for astatine. If there were, it would just be the word "NO" scrawled over and over in charred blood.
    -- Randall Munroe, "What If?"
  ```

* The second is a binary index file with the same name as the text file and a `.dat` extension.

There is a command-line interface for this plugin that will generate these `.dat` files for you. From the root folder of your Grav installation, type the following:

```bash
bin/plugin fortune index path/to/files
```

You can provide a single file name or point to a folder, in which case it will index (or reindex) all files in that folder (*not* recursively). This folder should only contain the text files and any pre-existing `.dat` files.

### Inserting Into Pages

The plugin exports a global Twig variable `fortune`. Simply insert it wherever you want. Here's what appears on [my demo page](https://www.perlkonig.com/demos/fortune), for example:

```markdown
twig_first: true
process:
    twig: true
never_cache_twig: true

---

You open the fortune cookie and find the following:

{{ fortune }}
```

If you use it in a page, you'll want `never_cache_twig` set to true if you want the quote to continually change. Otherwise the quote will get cached and not change. 

If you have any problems, let me know!

## Credits

This plugin relies on [a library created by Henrik Aasted Sorensen](http://www.aasted.org/quote/). Many thanks!
