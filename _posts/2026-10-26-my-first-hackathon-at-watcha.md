---
title: "My First Hackathon at Watcha 2026"
date: 2026-10-26 21:00:00 +08:00
categories:
  - life
tags:
  - watcha
  - hackathon
  - tianxi
  - agent-skills
  - auto-organizer
  - experience
toc: true
---

I spent 24–25 October at [Watcha 2026](https://dahui.watcha.cn/) in Hangzhou's Longwu tea-town halls. The official line was "watch creation happen." For me it was simpler: walk the whole hall, try products I had only followed online, sit in a few talks — and finally enter a hackathon.

I had already been following a lot of AI products on the Watcha community — software as much as hardware. On site I spent a lot of that time with OPCs (one-person companies) and with promo people from some of the companies: what they claimed as an advantage, how the product actually works, and how they make money. I wanted those pieces so I could move them onto things I want to build.

![Watcha booth at the 2026 conference](/assets/img/posts/watcha-2026-booth.png)

![Watcher badge and merch at 猹话会](/assets/img/posts/watcha-2026-badge.png)

## Two days in the hall

The expo pass covered 100+ booths across six tracks. I walked the whole hall.

I was not hunting for a particular brand. **Alipay's AI glasses** and **Ascentiz's powered exoskeleton** happened to be there, so I tried them. On the glasses I used the nod-to-pay feature. The exo has some weight; after I ran a lap, I could still feel my thighs being lifted — that leftover inertia. Around them sat a lot of other AI software and hardware — docks, wearables, agent demos, things that want to live on a desk or in a pocket. I also walked out with more gifts than I planned: a Watcha blind-box, Lenovo's Xiangbangbang mouse, Xiaomi's HachimoDock, and a pile of smaller bits.

I sat the on-site **AI exam** as well: 50 questions. I scored **96 / 100** and got the AI Pioneer certificate.

On the morning of the 25th I went to the [Alipay AI Pay forum](https://watcha.cn/activities/dahui2026-aipay). That is where I learned how an AI product can take in revenue more easily. I also went to the [Founder AMA](https://watcha.cn/activities/dahui2026-expo). I still came away with a lot from listening.

The afternoon was the part I had been waiting for.

## Ninety minutes, first hackathon

The [Tianxi hackathon](https://watcha.cn/activities/dahui2026-lenovo) asked everyone to build a **Skill**, upload it to Lenovo's developer platform, and then pitch. Official time: **90 minutes**. You got **five minutes** on stage.

I wanted to build a file auto-organizer. I like organizing. For people who run events, sorting files is important and tedious. The idea was also simple enough to ship under a time limit. I planned to use Cursor, the stack I already live in.

The hall Wi-Fi disagreed.

Cursor would not stay usable, so I downloaded **Tianxi AI** on the spot. They wanted to promote it.

I lost the thread **twice**.

The first time, I had just installed the app and started building. I was close to a working Skill. Then a login wall popped up. After I signed in, the history was empty. The conversation I had been living in was gone.

The second time, I rebuilt enough of the work to keep going — and then noticed the default chat mode cannot call tools. I switched to Super mode. That opened a **new session**. The old one was still there, somewhere else. I stayed in the Super mode window and finished the Skill there.

I almost quit. I submitted anyway, and I still signed up to pitch.

![Building the Skill in the hall](/assets/img/posts/watcha-2026-hackathon-coding.png)

## What I actually built

The Skill is [auto-organizer](https://github.com/Universe-ustc/auto-organizer): an Agent Skill that sorts a local folder by topic.

The pain is ordinary. A desktop or a grant folder fills up — PDFs, photos, scans, slides — and "I will tidy this later" never happens. Auto-organizer is not a magic classifier in one click. The **scripts** scan, move, write a report, and roll back. The **Agent** reads filenames and file text, proposes a folder tree, and only moves files after you say yes.

Defaults I care about:

- dry-run first; nothing moves without a confirm
- stay inside the folder you named
- never delete; never overwrite (it adds `(2)`)
- skip `.git`, dotfiles, and `.env`
- identical files (SHA-256) get flagged; one copy stays in the topic folder, the rest go to a duplicates bin
- optional PDF text and Tesseract OCR if those tools are on the machine

That is a personal-office Skill, which matched the hackathon track. The on-site version was rough. What is on GitHub now is the version I cleaned up after I got home.

## Five minutes, a Feishu doc

Other people who pitched had also hit bugs. They still showed up with a Skill **and** a deck — PPT or a small HTML page, mostly made with AI, and they looked polished. I tried to make slides in Tianxi AI. It was too slow. I gave up and pitched from a **Feishu doc**.

![Pitching auto-organizer at 猹话会](/assets/img/posts/watcha-2026-hackathon-pitch.png)

The room voted. I did not place. That was the expected ending for a first hackathon pitched from a document.

I posted the stage photo to WeChat Moments anyway. A second-year graduate student asked if there was a GitHub link — she said the idea would actually help her. That question is why I finished the repo instead of leaving it as a 90-minute draft.

If you also have a messy folder and an Agent that can load Skills, the package is here: [github.com/Universe-ustc/auto-organizer](https://github.com/Universe-ustc/auto-organizer).

I did not win. I did leave with a first hackathon, a Skill I still use, and a clearer sense of how strong other people's creativity and hands-on work can be.
