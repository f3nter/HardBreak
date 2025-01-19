# How to contribute

Thank you for your interest in contributing to our GitBook project! Your efforts help to create valuable, high-quality content for everyone who relies on this resource. Before you get started, here are a few important guidelines.

## Get started 🚀[​](https://www.thehacker.recipes/contributing#get-started) <a href="#get-started" id="get-started"></a>

1. Fork the repository ([https://github.com/f3nter/HardBreak/fork](https://github.com/f3nter/HardBreak/fork)) to your account
2. Make the changes you want in your forked HardBreak repository, respecting the guidelines below
3. If your changes are ready, make a Pull Request ([https://github.com/f3nter/HardBreak/compare](https://github.com/f3nter/HardBreak/compare))\


    <figure><img src="../.gitbook/assets/image (85).png" alt=""><figcaption><p>Select the original f3nter HardBreak main branch on the left and your updated branch on the right.</p></figcaption></figure>
4. Your changes will be reviewed as soon as possible and implemented in HardBreak

## Things to Consider Before Making Changes

1. Check for Existing Pages\
   Before creating a new page or section, please verify whether a page covering your topic already exists. If yes, consider adding your content to the existing page to maintain coherence and avoid duplication.&#x20;
2. Contributing to Existing Pages\
   When contributing to an existing page, ensure that your additions are seamlessly integrated into the existing content. This helps maintain flow and structure.

#### Guidelines for Contributing to Pages

1. **Proper Structure**\
   Each page should follow a logical and clear structure that aids both learning and reference. We recommend organizing content into sections like:
   * Theory: Provide the background or conceptual explanation of the topic.
   * Cheat Sheet: If possible provide a list of a summary of commands/information
   * Usage: Include practical applications, examples, or step-by-step guides.
   * Resources: List any external references, related tools, or further reading.
2.  **Citing Other Authors**

    {% hint style="warning" %}
    If you are incorporating content from another source or author, make sure to credit them in the Resources section. This not only maintains transparency but also respects the intellectual contributions of others.
    {% endhint %}

    When you use a picture from another author: Put the source in the caption, like : "Source:\<link>"
3.  **Don't use pictures from other sources than your own**

    The copyright is very strict, when it comes to copying pictures from other sources. Only use your own pictures.
4. **Language Style**\
   Please write in a style that strikes a balance between accessibility and professionalism. The goal is to make the content understandable for a broad audience while retaining an authoritative tone. Aim for clarity, avoiding overly technical jargon where possible, but still providing depth where needed.
5. **Make It Useful for Both Beginners and Experts**
   * For Beginners: Ensure that your content introduces new topics in a way that is easy to follow, providing enough context and explanation for users who are unfamiliar with the subject.
   * For Experts: Include details like key commands, configurations, or technical insights that will help more experienced users quickly find the information they need.
6. Check out the [Gitbook - Basics](gitbook-basics/), which include some markdown hacks like hints, tabs, callouts etc.
   1. Example Tabs:
   2.  Markdown code

       ```markdown
       {% raw %}
       {% tabs %}

       {% tab title="Windows" %} Here are the instructions for Windows {% endtab %}

       {% tab title="OSX" %} Here are the instructions for macOS {% endtab %}

       {% tab title="Linux" %} Here are the instructions for Linux {% endtab %}

       {% endtabs %}
       {% endraw %}
       ```

       Result:

{% tabs %}
{% tab title="Windows" %}
Here are the instructions for Windows
{% endtab %}

{% tab title="OSX" %}
Here are the instructions for macOS
{% endtab %}

{% tab title="Linux" %}
Here are the instructions for Linux
{% endtab %}
{% endtabs %}

## Adding a new page

If you want to contribute an entirely new page, please update the [SUMMARY.md](https://github.com/f3nter/HardBreak/blob/main/SUMMARY.md) file and include your page in the desired chapter/section. This file is used by GitBook to structure the website. If you do not add your page in the SUMMARY.md file, it won't get displayed on the HardBreak website.
