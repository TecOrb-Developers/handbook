## Turbo Frames Rules

#### Rule 1 of `turbo_frame_tag`

- When clicking on a link within a Turbo Frame, Turbo expects a frame of the **same id** on the **target page**. 
- It will then replace the Frame's content on the **source page (current page)** with the Frame's content on the **target page**.
- let's wrap a piece of the Articles#new page (piece means we want just new form here on click of New Article) in a Turbo Frame of the **same id**. 
- So We have to set form within turbo_frame_tag the same id "new_article_turbo_frame"

[Here is the commit to implement Rule 1](https://github.com/TecOrb-Developers/rails-hotwire-turbo/commit/6083b88d354fe8bde720e31d253cac78bf9092b5)

#### Rule 2 of `turbo_frame_tag`

 When clicking on a link within a Turbo Frame, if there is no Turbo Frame with the same id on the target page, the frame disappears, and the error Response has no matching `<turbo-frame id="name_of_the_frame">` element is logged in the console.

[Here is the commit to implement Rule 1/2](https://github.com/TecOrb-Developers/rails-hotwire-turbo/commit/5f61f21b42d9e0f1b5fd290952417e8cf1234c11)

#### Rule 3 of `turbo_frame_tag`

A link can target another frame than the one it is directly nested.

Here we are adding `data: { turbo_frame: "second_frame" }` to link_to which is already nested with 'new_article_turbo_frame'.

In that case, the Turbo Frame with the same id as the data-turbo-frame data attribute (link tag) on the source page (Table's second_frame) will be replaced by the Turbo Frame of the same id as the data-turbo-frame data attribute on the target page (New article form's second_frame).

Example: click on the "New Article" button. We should see our articles list (which is in second_frame) will be replaced by the new article form's 'second_frame' section. This is because our link now targets the second frame.


[Here is the commit to implement Rule 3](https://github.com/TecOrb-Developers/rails-hotwire-turbo/commit/06b60af40b243412af6d4b0fcf354800a22f7199)

#### Special frame `_top`

- If we wanted our "New Article" button to replace the whole page, we could use `data-turbo-frame="_top"`.

- When using the `"_top"` keyword, the URL of the page changes to the URL of the target page, which is another difference from when using a regular Turbo Frame.

- Browser will replace the whole page from the top with new article page

- Every page has frame `"_top"`  by default

[Here is the commit for using "_top" ](https://github.com/TecOrb-Developers/rails-hotwire-turbo/commit/98ab333975bab49b7badec03a90f2a6479e7975c)
