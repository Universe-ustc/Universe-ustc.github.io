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

I spent 24–25 October at [Watcha 2026](https://dahui.watcha.cn/) in Hangzhou's Longwu tea-town halls. The official line was "watch creation happen." For me it was simpler: walk the floor, try the hardware I had only seen in videos, sit in a few talks — and finally enter a hackathon.

![Watcha booth at the 2026 conference](/assets/img/posts/watcha-2026-booth.png)

I had the Watcher badge, a pixel-bear lanyard, and two full days. That already felt like enough of a souvenir. The rest of the weekend was louder.

![Watcher badge and merch at 猹话会](/assets/img/posts/watcha-2026-badge.png)

## Two days on the floor

The expo pass covered 100+ booths across six tracks. I did not try to "finish" the hall. I drifted, talked, and put my hands on things.

Two I had wanted to try for a long time: **Alipay's AI glasses**, and **Ascentiz's powered exoskeleton**. Both are the kind of product that looks obvious in a clip and slightly strange on your own face or back. Around them sat a lot of other AI software and hardware shapes — docks, wearables, agent demos, things that want to live on a desk or in a pocket. I also walked out with more gifts than I planned: a Watcha blind-box, Lenovo's Xiangbangbang (想帮帮) mouse, Xiaomi's HachimoDock, and a pile of smaller bits.

I sat the on-site **AI exam** as well. 50 questions from Watcha's instructors. I scored **96 / 100** and got the AI Pioneer certificate. That was a nice, concrete stamp in a weekend that was otherwise all motion.

On the 24th I went to the [Alipay AI Pay forum](https://watcha.cn/activities/dahui2026-aipay) — *from code to the first bucket of money* — and the [Founder AMA](https://beating.news/events/461707) on how a product actually gets made. I did not take neat notes. I mostly wanted to hear people who ship, not people who only talk about models.

The 25th afternoon was the part I had been waiting for.

## Ninety minutes, first hackathon

The [Tianxi hackathon](https://watcha.cn/activities/dahui2026-lenovo) — "Super Partner, crash course" — asked everyone to build a **Skill**, upload it to Lenovo's developer platform, and then pitch. Official time: **90 minutes**. Official sponsor: Lenovo / Tianxi AI. First place later walked off with a mini host PC. Scoring was not a judge panel. You got **five minutes** on stage; the room voted with paddles. No Q&A.

My plan was boring and safe: use Cursor, the stack I already live in, and ship something I actually need.

The floor Wi-Fi disagreed.

Cursor would not stay usable, so I did what the sponsor hoped people would do. I downloaded **Tianxi AI** on the spot. Lenovo was pushing it hard; it is supposed to be the on-device "super partner." In those 90 minutes it felt like an unfinished product that had been asked to host a contest.

I lost the thread **twice**.

The first time, I had just installed the app and started building. I was close to a working Skill. Then a login wall popped up. After I signed in, the history was empty. The conversation I had been living in was gone.

The second time, I rebuilt enough of the work to keep going — and then noticed **Turbo mode cannot call tools**. I switched to Super mode. Super mode opened a **new session**. The old one was still there, somewhere else. I had to start again in a third window.

I was close to walking out. Then the simpler thought won: I had come all this way, and this was my first hackathon. I submitted whatever I had, and I still signed up to pitch.

![Building the Skill on the hackathon floor](/assets/img/posts/watcha-2026-hackathon-coding.png)

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

## Five minutes, a Feishu doc, no prize

Other people who pitched had also hit bugs. They still showed up with a Skill **and** a deck — PPT or a small HTML page. I tried to make slides in Tianxi AI. It was too slow. I gave up and pitched from a **Feishu doc**.

![Pitching auto-organizer at 猹话会](/assets/img/posts/watcha-2026-hackathon-pitch.png)

The room voted. I did not place. That was the expected ending for a first hackathon pitched from a document.

I posted the stage photo to WeChat Moments anyway. A junior student asked if there was a GitHub link — she said the idea would actually help her. That question is why I finished the repo instead of leaving it as a 90-minute draft.

If you also have a messy folder and an Agent that can load Skills, the package is here: [github.com/Universe-ustc/auto-organizer](https://github.com/Universe-ustc/auto-organizer).

I did not win a mini PC. I did leave with a first hackathon, a Skill I still use, and a clearer sense of what "ship in 90 minutes on someone else's stack" feels like. Next time I will bring a local toolchain that does not need the venue Wi-Fi — and a backup way to make slides that is not the same app that just ate my context.
