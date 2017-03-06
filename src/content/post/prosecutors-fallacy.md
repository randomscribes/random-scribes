+++
image = "elasticsearch.png"
date = "2017-03-05T13:39:15-06:00"
title = "Prosecutors Fallacy"
draft = true

+++

What is Prosecutors Fallacy?

In its simplest form is faulty reasoning, usually statistical, used by prosecutors. Really if you understand the two seperate terms _prosecutor_ and _fallacy_ the term is pretty simple to understand. The fallacy derives from the court system when oneside (there's also the concept of defencey attorney's fallacy) makes an argument that oversimplies some statistical inference and incorrect states the odds of guilt (or innosence).

## Examples
### Conditional Probability
Let's assume that the owner of a convienance store wins the lottery from a ticket that came from her store. Fishy eh? Well the Crown through it was fishy too. So the charged the store own with fraud. The prosecutor argues that because the chances of winning the lottery are so small, let's say 1 out of a 10 million, that the store owner must have modified her chances in order to actually win. However given the number of people who play the lottery, the probably of someone winning it is quite high.

### Berkson's Paradox
In a famous British case. The mother of two children who both died as early infants (11 weeks and 8 weeks) was accused of murdering them. She was convicted, in part because of the expert testimony of paediatrician that testified that the probability of two children in the same family dying from SIDS is about 1 in 73 million. However this was based off the assumption that the deaths were independant (e.g. having one child die of SIDS doesn't increase the probablity of having another child die of SIDS). It turns out that there isn't independance, parents who have one child die of SIDS do have an increase likeliness to have another die. There's also the argument that having two infants being murdered is also very unlikely just like both of them dying from SIDS. Niether of these two arguments were brought up at trial.

The woman was originally convicted, but appealed and was eventually acquitted after three years in jail. Tragically, she developed numerous psychiatric problems and died of alcohol poisoning.

### Multiple Comparisons
DNA evidence can also lead to the prosecutor's fallacy. Let's say DNA evidence is compared to a database that contains a 100,000 samples. In this example a match is made with an expert witness testifying that the probability of a matching profile being made is 1 in 50,000. This database had 100,000 observations. So that means that 100,000 possible matches. We'd expect that there would even be 2 matches. The probability of getting at least 1 match in the database would have been: 

1 - (1 - (1 / 50000)) ^ 100,000 = 86.47%

Without other evidence, this match could have just been do to chance.

## Business Examples
While researching this I struggled to come up with _business_ examples of the prosecutor's fallacy. I think it's because at it's heart this fallacy is just incorrect reasoning used be prosecutors. So really the business examples that I would be looking for would just be ways that business use faulty reasoning. Most of the time in business you don't have cases where you have a prosecutor and a defendant, at least in healthy organizations. With that in mind I did come up with a few scenerios that I could see occuring:

### HR
Let's say that 1 out of 100 people lie about their work history on their resume. A new tech startup was hired to automatically read resumes and filter resumes that are untruthful. They have a 5% false positive rate. HR was enthusiastic with the results. They stopped themselves from hiring 10 potential candidates in the first month. The director of HR was so enthusiastic, he wanted to run all of their existing employees through the system and discipline any of those that lied. 200 existing employee resumes were tested. Kelly's resume was flagged. What's the probability that Kelly actually lied on her resume? Well because of the 5% false positive rate, we'd expect 10 people (200 * .05) to be incorrectly flagged as lying. Since only 1 out of 100 people lie about their work history, only 2 employees (.01 * 200) actually did. So even if Kelly is flagged she still only has a 20% (2 / 10) chance of actually lying on her resume.

### Marketing
1 out of every 10 leads are considered a _big fish_. Big Fish have an average annual contract value of $1,000,000 while regular leads have an annual contract value of only $50,000. The company's goal is to increase annual revenue by $10 M. 5% of leads close. According to this information, one would expect to hit the $10 M goal with:

10,000,000 / ((.1 * 1,000,000 + .9 * 50,000) * .05) = 1,380 leads (round up)

At the end of a year, marketing provided 1,500 leads to sales. Unfortunately, the company missed their sales target by a staggering $4.15 M. During an executive meeting, the CMO and CRO get in an argument of who's fault it is that they missed their sales target. The CRO eventually concedes having no evidance to refute marketings claims. She returns to the sales floor expected that her time with the company may be coming to an end. However a couple of recent university grads who are working as interns in the sales department heard about the numbers that marketing came up with. They were shocked, everything seemed to be going well on the sales floor. Close rate hasn't dipped, their annual contract value event increased by 20% compared to last year. They realize a missing piece in marketing's reasoning, not all leads close at the same rate. Big Fish close at a rate of 1%. They update the calculation:

10,000,000 / ((.1 * 1,000,000 * .01 + .9 * 50,000 * .05)) = 3,077 leads (round up)

They quickly report their findings to the CRO, immediately lifting the CRO's spirit. She never really liked the CMO anyway.


## Wrapup
As you may have noticed, the examples that I have provided are just fallacies. Prosecutors Fallacy is really just a fallacy that's done in an accusatory way.

Much of this post was based on the [Wikipedia Article on Prosecutor's Fallacy](https://en.wikipedia.org/wiki/Prosecutor's_fallacy)

image: http://www.publicdomainpictures.net/pictures/170000/velka/judge-gavel-1461998753I40.jpg
