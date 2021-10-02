# Carolina Data Challenge 2021 Site

## Folder Structure

- `index.md`
  - This is the main landing page.
    It contains some basic info about the project and us and links to the other pages.
  - When adding a link to your notebook, do so in the following way:
    ```
    1. [Link Text]({{ site.baseurl }}{% link notebook_name.md %})
    ```
- `some_notebook.md`

  - Notebooks converted to markdown should be in the project root. After converting, you need to add the following to the top of of the file:
    ```
    ---
    title: Your Title
    ---
    ```
  - Additionally, you'll need to change any references to images from the converted file to reference the `assets` folder, likely in the following form
    ```
    ![image_name]({{site.baseurl}}/assets/notebook_folder/image_name.png))
    ```
  - Sometimes when converting from notebook to markdown, the convert will unnecessarily add spaces between lines. This can be annoying for code, so it's probably a good idea to fix that.
  - If you'd like to remove any cells from the notebook, you can do so by simply removing them from the markdown. This can be useful for showing only the code or outputs that are necessary/unique to the notebook.
  - You can write inline HTML in the converted notebook files, which should enable embedding things that the automatic coversion doesn't handle too well. You can separate the HTML into its own file and do the following to insert it.
    ```
    {% include html_file.html %}
    ```
    The HTML file should be in the `_includes` folder.

- `assets/`
  - This folder contains all the assets (pictures mostly) used in the site.
  - It's reccomended that you create subfolders for each notebook, and place the images in the subfolder. Running the Jupyter to markdown conversion will automatically create a folder for each notebook.
