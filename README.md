## Introduction

![A sample grid of 10 images contained in Simulacra Aesthetic Captions](https://github.com/JD-P/simulacra-aesthetic-captions/blob/main/sacDemoGrid.png)

Simulacra Aesthetic Captions is a dataset of over 238000 synthetic images generated
with AI models such as [CompVis latent GLIDE](https://github.com/CompVis/latent-diffusion)
and [Stable Diffusion](https://github.com/pesser/stable-diffusion) from over
forty thousand user submitted prompts. The images are rated on their aesthetic value from 1 to
10 by users to create caption, image, and rating triplets. In addition to this
each user agreed to release all of their work with the bot: prompts, outputs,
ratings, completely public domain under the [CC0 1.0 Universal Public Domain Dedication](https://creativecommons.org/publicdomain/zero/1.0/).
The result is a high quality royalty free dataset with over 176000 ratings that
can be used for projects such as:

* Filtering Datasets
* Guiding Generative Models
* Training A Prompt Generator
* Extracting vitamin phrases ("trending on artstation", etc)
* Alignment Research

Because earlier versions of [SimulacraBot](https://github.com/JD-P/simulacrabot)
used a separate upscaler to make latent
GLIDE outputs palatable to users the dataset also includes limited contrastive
data. It consists of which images were chosen to be upscaled from each batch
with 12,648 samples, or about 2000 batches. The resulting upscaled images are
not included in the dataset.

## Notable Uses

An early version of Simulacra Aesthetic Captions was used to
[create LAION Aesthetic](https://github.com/LAION-AI/laion-datasets/blob/main/laion-aesthetic.md),
a version of LAION 5b filtered using around 4000 ratings.

Special thanks to [Victor Weaver](https://github.com/victorweaver) (twitter: [@_victorweaver](https://twitter.com/@_victorweaver)) for his early feedback and suggestions on the bot, as well as writing the initial public domain prompt and rating dataset that allowed us to make LAION-aesthetic as early as we did.

## Download

The index of Simulacra Aesthetic Captions is a sqlite database containing all
information and metadata besides the images themselves:

```curl -OL https://raw.githubusercontent.com/JD-P/simulacra-aesthetic-captions/main/sac_public_2022_06_29.sqlite```

The images in version 1.0 of Simulacra Aesthetic Captions can be downloaded from
their bucket with the following cURL command:

```curl -OL https://s3.us-west-1.wasabisys.com/simulacrabot/sac.tar```

### Suggested Citation

If you use Simulacra Aesthetic Captions in your published work we suggest the following citation:

```
@techreport { pressmancrowson2022 ,
author = { John David Pressman and Katherine Crowson and Simulacra Captions Contributors } ,
year = 2022 ,
title = { Simulacra Aesthetic Captions } ,
institution = { Stability AI } ,
type = {} ,
number = { Version 1.0 } ,
note = {\ url { https://github.com/JD-P/simulacra-aesthetic-captions }}
}
```

## Generation Methods

SimulacraBot has used multiple generation methods over its lifetime, and will
continue to use new ones in the future. Each generation method is defined as a
model inferenced with a specific set of parameters. If the parameters change the
method number should be incremented for generations done with that method. For
reference here is every generation method used over SimulacraBot's lifetime,
even though only 2 and 3 appear in the dataset as currently released.

|Method #| Method Name/Arts Media
|--------|-----------------------
|0       | [CLOOB Conditioned Latent Diffusion](https://github.com/JD-P/cloob-latent-diffusion)
|1       | CLIP Guided CLOOB Conditioned Latent Diffusion
|2       | [CompVis latent GLIDE](https://github.com/CompVis/latent-diffusion)
|3       | [latent Imagen 512x512](https://github.com/pesser/stable-diffusion)
|4       | latent Imagen f16 768x768 cond scale 4
|5       | latent Imagen f16 768x768 cond scale 5
|6       | latent Imagen f16 768x768 cond scale 6
|7       | latent Imagen f16 768x768 cond scale 7
|8       | latent Imagen f16 768x768 cond scale 8
|9       | latent Imagen f16 768x768 cond scale 9
|10      | latent Imagen f16 768x768 cond scale 10

## Simulacra Aesthetic Survey

The initial design of Simulacra Aesthetic Captions called for collecting all
ratings into an anonymous pool. However during data collection it was observed
that some users would downrate objectively well drawn pictures because they're
"scary", or included public figures they didn't like such as the US president.
Some users would also ignore rating instructions to downrate watermarks and other
marks that encroach on the canvas of the output. Rather than try to force people
to go against their intuition, which seemed somewhere between tyrannical and futile,
an aesthetic survey was implemented on signup that records users behavior around
these confounding factors in aesthetic judgment. The survey currently consists of
20 questions in the form of 1-10 ratings of fixed hand chosen images that each
represent either a conjectured component of human aesthetic judgment or a bias
that users of the dataset would like to be able to handle during their analysis.
This survey data also enhances the possibility of using Simulacra Aesthetic Captions
for general research into human aesthetic preferences by e.g. deriving clusters
of human aesthetic judgment. The images and their associated captions are shown
below:

![The 20 images in the first Simulacra Aesthetic Survey. The images are arranged in a grid in rows of 5 and correspond to text descriptions in the table below starting at image 0 and going left to right ending at image 19 in the bottom right corner.](https://github.com/JD-P/simulacra-aesthetic-captions/blob/main/sacSurveyGrid.png)

|#  | Prompt/Description                                                         | Component
|---|----------------------------------------------------------------------------|--------
|0  | The West Coastline. #west #ocean                                           | Nature photo
|1  | hyperrealistic bokeh portrait cinematic matte painting concept art african american New Orleans | Ethnic art/Racism
|2  | A painting of a swamp at low tide. There is a small portion of a castle and a patch of blue sky in the far off distance. | Watermarked
|3  | fantasy illustration of a river of blood, flowing through a field of bones.| Wrong caption
|4  | full color inkscape digital art of a hackers lair bedroom computer setup battlestation | Weak prompt fit 
|5  | traditional dark Hijab Muslim Woman Islam Girl Portrait Fashion People Model Eyes oil on canvas | Islam Sentiment
|6  | accurate beautiful cute anime symmetric danbooru chibi depiction of a magical girl | Anime
|7  | A portrait painting of Adolf Hitler                                        | Quality vs. Subject
|8  | detailed accurate krita digital masterpiece commissioned street scene of a cyberpunk Tokyo market stall, artstation matte painting | Urban/Modern
|9  | professional HDR flambient golden hour real estate photography of futuristic hyperrealism scifi fantasy industrial corporate agents | two images vertically split
|10 | The colors in this illustration are simply gorgeous! They perfectly compliment the scene and add an extra layer of beauty to the already stunning image! | Calming vs. Canvas encroachment
|11 | hyperrealism chiaroscuro cinematic oil on canvas matte painting of professional golden hour flambient real estate photo scifi traditional japanese onsen shinto temple zen garden | Canvas encroachment
|12 | I found this abstract art and don't know what it means | Canvas encroachment
|13 | A painting of a mystical creature in a magical forest | Fantasy/Witch
|14 | digital painting of a mansion in the middle of a forest, 4k, Ross Tran, Gurney, Frank Frazetta, Skeeva, Gal Barkan, matayosi, high fantasy concept key art | Landscape/Fancy house
|15 | professional HDR flambient wide angle bokeh photography of a cute pink glittery magical fairy enchanted forest fantasy butterflies and poodles | Cute/Feminine
|16 | chiaroscuro professional oil on canvas matte painting concept art of a masculine warrior from myths and legends | Heroic/Masculine
|17 | A nightmarish creature made of shadows and teeth. | Scary vs. Well Drawn
|18 | A crowded subway car, the fluorescent lights flickering and casting an eerie glow on the people inside. | Melancholy/Modern/Artistic vs. Blurry
|19 | krita digital masterpiece of the tower of babel as a series of neural net layers | Esoteric

A unique combination of ratings on the aesthetic survey also serves as a synthetic
user ID through the dataset. This was done to balance privacy against being able to
get at the aesthetic preferences of coherent agents versus an averaged out mush.
Unfortunately due to a bug in earlier version of SimulacraBot, some aesthetic surveys
were corrupted with more than 20 entries. It is not known exactly what caused this or
what the ratings are supposed to be, so it may be preferable to exclude these surveys
from analysis that relies on the survey to make its conclusions.

## Table Of Biases By Relevant Use Case

Simulacra Aesthetic Captions has many biases in its portrait of human aesthetic
preferences. The relevant biases for different use cases are summarized in the
tables below.

The level of concern for the bias on the use case has been marked with 0-3 X's.
With no X being almost no concern and three X's being something the user will
probably make a mistake if they don't think carefully about.

|Use Case        |NSFW|Copyright|Hate|WEIRD|'Techies'|Surveillance|
|----------------|----|---------|----|-----|---------|------------|
|NSFW Filter     | XXX|         |  XX|     |         |     XXX    | 
|Dataset Curation| XX |    XX   |  XX|  XX |   X     |            |
|Model Inference | XX |    XXX  |  X |  XX |   X     |     X      |
|AGI Alignment   | XXX|    XX   | XX |  XXX|   XX    |     XXX    |

|Use Case        |Model.B|UserFixations|GradeCurve|Participation.Eq|UpscaleBug|
|----------------|-------|-------------|----------|----------------|----------|
|NSFW Filter     |   XX  |             |          |                |          |
|Dataset Curation|   XXX |      XXX    |    X     |        XX      |          |
|Model Inference |   XXX |      XXX    |    XX    |        X       |          |
|AGI Alignment   |   XXX |      XXX    |    XX    |        XXX     |    X     |

## List Of Biases With Explanations

### No NSFW

Because Simulacra Aesthetic Captions does not intentionally contain NSFW entries,
it is missing a key component of human aesthetic values and experience. Unfortunately
the challenges of collecting a dataset like this from users at scale were considered
too perilous for a first release. It is likely that a NSFW supplement to Simulacra
Aesthetic Captions would be collected as a separate dataset that could be added
onto the main body of SAC.

The guidance given to users on what constitutes 'NSFW' was as follows:

```
What is NSFW?

NSFW basically means:

- Excessive gore/blood/etc
- Licentious nudity, nudity that exists to suggest sex including sexualized poses, etc
- Sex. Anything that involves actual sex or sex acts is way over the line, never deliberately submit prompts that involve this.

To get pedantic about nudity, if it's fantasy art depicting bare nipples but otherwise not licentious it's probably fine. If it depicts a penis or vagina it is probably not fine, but exceptions might be made. Avoid deliberately submitting prompts involving nude figures. As a stock example of nudity which is not NSFW, the Rider-Waite depiction of The Star is nude, but it is not lewd or licentious.

Also note that something doesn't need to be nude to be removed as sexually NSFW. A sufficiently trashy prompt/image combo can and will be removed. "Slut looking at you from across the bar", things like that.
```

### No copyrighted content

The lack of copyrighted content in Simulacra Aesthetic Captions bars models
trained with it from a full understanding of pop culture. Because mass culture in
Western countries largely consists of specific copyrighted content, models that rely on SAC
as their ground truth for any aspect of their function will have that functionality
impaired when handling popular culture.

### No hate speech

For compelling reasons hateful content is excluded from Simulacra Aesthetic
Captions. However hatred of others and reactions to that hatred are undeniably
part of human values. Even if we find it so abhorrent as to place it into some
other category, the paradox of tolerance involves hatred and not tolerating the
intolerant is a major value of contemporary Western society. Because the dataset
lacks hate or reactions to hate users who would like to use SAC as part of
their moderation suite will probably find it lackluster. While a "Hateful 
Aesthetic Captions" might be a useful supplement for moderation suites and
AGI alignment, it's not clear where a population of users could be found who
would cooperate with the intent of such a dataset while producing
authentic samples. Furthermore the benefits of releasing such a dataset would
have to be weighed against the impact to other people of making large amounts
of such content high quality, curated, and freely available even for legitimate
academic purposes.

### Participants Are WEIRD

Participants in Simulacra Aesthetic Captions are largely [WEIRD]https://www2.psych.ubc.ca/~henrich/pdfs/WeirdPeople.pdf),
or Western, Educated, Industrialized, Rich, and Democratic. This means that the
aesthetic preferences recorded are not universal among humanity. While we didn't
take a survey of the demographic makeup of SimulacraBot users, it should be
assumed they largely reside in the United States and Europe. We welcome
replications of Simulacra Aesthetic Captions which sample their results from
other locales and demographics.

### Users Are Mostly Open Source AI Developers And Enthusiasts

Further narrowing the scope of aesthetic feedback in Simulacra Aesthetic Captions
is the userbase consisting largely of people who are power users and developers
of AI art. This means that their aesthetic feedback is going to lean STEM, fantasy,
nerdy, esoteric, etc.

### Surveillance

Because users write their prompts in the presence of other people, they are going
to avoid "guilty pleasures" and other topics on which they might be judged. This
means that anything which might only be expressed anonymously or in private is
less likely to appear in Simulacra Aesthetic Captions.

### Model Biases

Users are naturally going to gravitate towards things the model is good at drawing.
Each generative model has a set of biases about what it is capable of drawing well,
users pick on these and tailor their prompt style to accomodate it. This means that
Simulacra Aesthetic Captions [only represents human preferences conditional on the
models biases](https://twitter.com/jd_pressman/status/1535700144011612161).

### Users Have Fixations And Narrow Interests

Some users of Simulacra Aesthetic Captions are only interested in having the model
draw a couple of things. For example one user really likes using the model to draw
a 'world tree', or the earth represented as a giant tree. These fixations and narrow
interests can become large parts of the dataset relative to their general importance.
Before using Simulacra Aesthetic Captions to filter a dataset, it may pay to look
closely at repeated prompts and themes to cull their numbers down to sane levels.

### Users Grade On A Curve

During discussions about rating, users repeatedly express a preference to
grade models on a curve. They give charity points to models where they know
they're lacking so they don't rate everything low. This means that different
methods probably have different rating distributions relative to the 'ground
truth' aesthetic preference of the image without the context of the model that
generated it.

### Buggy Upscaling

During the period that SimulacraBot offered upscaling, it had a bug when multiple
users used the bot that meant the author of a prompt had to 'race' to open their
upscale menu first if they wanted to upscale their outputs. This race condition
probably had subtle effects on the distribution of images found in the upscaled
data.

### Unequal Participation

[Like most services](https://en.wikipedia.org/wiki/1%25_rule), SimulacraBot usage
is on a power law where a small minority of the nearly 400 users contribute the
vast majority of the content. This means that while in theory the ratings and
prompts are contributed by many people, in practice a handful of users aesthetic
preferences dominate the dataset.