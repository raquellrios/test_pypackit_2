---
sd_hide_title: true
html_theme.sidebar_secondary.remove:
---
# {{pp_meta.name}}

:::{toctree}
:includehidden:
:hidden:
:numbered:
intro/index
manual/index
news/index
contribute/index
about/index
help/index
:::


{% for theme in ["light", "dark"] %}
:::{image} _static/logo_full_{{theme}}.svg
:alt: {{pp_meta.name}}
:align: center
:class: only-{{theme}} homepage-logo
:::
{% endfor %}

---

{.element-in-page-without-sidebar}
{{ pp_meta.description.replace(pp_meta.name,
"[{}]{}".format(pp_meta.name, "{.project-name}"), 1) }}


<div class="element-in-page-without-sidebar">

:::{button-ref} intro/overview/index
:ref-type: myst
:color: primary
:expand:
:class: homepage-button

[Key Features]{.homepage-button-text}
:::

</div>


::::{card-carousel} 2
:class: element-in-page-without-sidebar
{% for point in pp_meta.keynotes %}
:::{card} {{point.title}}
:class-title: sd-text-center
{{point.description}}
:::
{% endfor %}
::::


<br>


<div class="element-in-page-without-sidebar">

:::{button-ref} intro/overview/index
:ref-type: myst
:color: primary
:expand:

[Learn More]{.homepage-button-text}
:::

</div>


::::{card-carousel} 1
:class: element-in-page-without-sidebar

:::{card} Intro: Discover the Essence of {{pp_meta.name}}
:link: intro/index.html
:img-top: /_static/img/icon/background.svg
:class-title: sd-text-center
:class-img-top: dark-light icon-image

Start off with the introduction section to learn more about
{{pp_meta.name}}'s motivations, objectives and capabilities.
This section offers a high-level overview of {{pp_meta.name}}, highlighting its main features,
the challenges they address, and the value they bring to your projects.
Serving as an excellent starting point for new users,
it also provides a summary of fundamental concepts and background information
that are essential to fully understanding and utilizing {{pp_meta.name}}.
:::


:::{card} Manual: Your Comprehensive Guide
:link: manual/index.html
:img-top: /_static/img/icon/user_guide.svg
:text-align: center
:class-img-top: dark-light icon-image

Dive into the user manual for in-depth information on the key concepts of {{pp_meta.name}},
along with detailed explanations of all its features and functionalities.
From step-by-step instructions on setting up {{pp_meta.name}} for the first time
and integrating it into your new or existing project,
to comprehensive guides on how to use its various features and functionalities
in your software development process,
the user manual covers everything you need to know
to fully leverage {{pp_meta.name}}'s capabilities.
:::

:::{card} News: Stay Informed with {{pp_meta.name}} Updates
:link: news/index.html
:img-top: /_static/img/icon/news.svg
:text-align: center
:class-img-top: dark-light icon-image

Check out our blog to stay up to date with the latest announcements
and developments of the {{pp_meta.name}} project.
This section keeps you informed about {{pp_meta.name}}'s new releases with detailed changelogs,
and provides insights into the project's roadmap
and the team's plans for the future of {{pp_meta.name}}.
Being the main source of information about {{pp_meta.name}}'s latest developments,
the news section is a full-fledged blog with RSS feed support that you can subscribe to,
so you never miss out on any important updates.
:::

:::{card} Contribute: Join the Community
:link: contribute/index.html
:img-top: /_static/img/icon/dev_guide.svg
:text-align: center
:class-img-top: dark-light icon-image

{{ pp_meta.name }} is a free and open-source project that can only survive
and grow through the help and support of great members like you.
If you are interested in joining the {{ pp_meta.name }} community,
head over to our contribution guide to learn more about how you can help.
From sharing your feedback and ideas or becoming a collaborator and helping us develop the project,
to spreading the word and helping us reach more people
or becoming a sponsor and supporting the project financially,
we highly appreciate all your contributions!
:::

:::{card} About: Unveiling the {{ pp_meta.name }} Story
:link: about/index.html
:img-top: /_static/img/icon/about.svg
:text-align: center
:class-img-top: dark-light icon-image

Learn more about the team behind {{ pp_meta.name }} and the project's history.
The About section offers insights into our mission, core values,
and the dedication driving {{ pp_meta.name }}'s success.
:::

:::{card} Help: Find Support When You Need It
:link: help/index.html
:img-top: /_static/img/icon/faq.svg
:text-align: center
:class-img-top: dark-light icon-image

The Help section is your go-to resource for assistance with any challenges you encounter.
Explore FAQs, troubleshoot common issues, and connect with our support team for personalized solutions.
:::

::::
