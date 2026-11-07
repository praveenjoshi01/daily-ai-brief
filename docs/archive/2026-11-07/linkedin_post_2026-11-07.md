5,000 agents. One repository. 7,200 pushes per second. (GitHub's internal tests, not yet shipped.)

Git didn't get faster. The write path stopped asking everyone to agree.

GitHub's new storage design, Project Rubicon, is worth reading if you run parallel coding agents. Agents are many writers, and the old design was built for a few careful ones.

The mechanism, sharply:

• Git objects go to Azure Blob Storage with no coordination between writers.
• Only the small reference update is ordered, through a replicated compare-and-swap log.
• Serving replicas are disposable caches; compaction runs on separate nodes.

Caveats: it's in limited private preview, the numbers are internal, and the post doesn't say how many branches the test used.

Question for builders: if you run parallel agents on one repo, how many distinct branches are active at once, and where does contention show up first?

Full breakdown with a redrawn write/read-path diagram: [link to Medium article]

(Tip: put the link in the first comment.)

#AIEngineering #AIAgents #Git #DeveloperExperience
