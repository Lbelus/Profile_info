# Profile_info

To convert a file from Markdown (`.md`) to a Word document (`.docx`), you can use several tools and methods. Here are some of the most popular options:

### 1. Using Pandoc

#### Steps:
1. **Install Pandoc**:
   - **Windows**: Download and install Pandoc from [the official Pandoc website](https://pandoc.org/installing.html).
   - **macOS**: Use Homebrew: `brew install pandoc`
   - **Linux**: Use your package manager, e.g., `sudo apt-get install pandoc` on Debian-based systems.

2. **Convert the file**:
   Open your terminal or command prompt and run the following command:
   ```sh
   pandoc input.md -o output.docx
   ```
   Replace `input.md` with the path to your Markdown file and `output.docx` with the desired path for your Word document.

### 2. Using an Online Converter
There are various online tools available that can convert `.md` files to `.docx` without requiring any software installation.

#### Example:
- **Convertio**:
  1. Visit [Convertio's Markdown to DOCX converter](https://convertio.co/md-docx/).
  2. Upload your `.md` file.
  3. Click "Convert".
  4. Download the converted `.docx` file.

### 3. Using a Markdown Editor
Some Markdown editors have built-in export functionality to convert Markdown files to Word documents.

#### Example:
- **Typora** (a popular Markdown editor):
  1. Open your `.md` file in Typora.
  2. Go to `File` > `Export` > `Word (.docx)`.
  3. Save the file.

### 4. Using Microsoft Word
Microsoft Word itself can open Markdown files and save them as `.docx`.

#### Steps:
1. Open Microsoft Word.
2. Go to `File` > `Open` and select your `.md` file.
3. Once the file is open, go to `File` > `Save As` and choose the `.docx` format.


### Troubleshoot

If the lists are unordered: 

You can use pandoc -t native to see how pandoc is parsing this. 
You'll see that the list is not parsed as a list. Why not? 
Well, pandoc's markdown requires a blank line before a list, to avoid false positives on lists (e.g. when a number followed by a period gets wrapped to the beginning of a line -- there was actually a test case like this in the original Markdown.pl test suite).
This requirement used to be common (following original Markdown.pl), but now that commonmark has allowed omitting the space, it is less common. See babelmark.
Anyway, the solution for you is to use ``-f commonmark`` or ``-f gfm`` or ``-f commonmark_x`` instead of the default ``-f markdown``.

Example:
```bash
pandoc -f commonmark FR_dossier_competence.md -o FR_dossier_competence.docx
```