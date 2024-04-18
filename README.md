# VS Code & Perl for Windows

I maintain a legacy code base at work and there is a serious lack of succinct documentation
to set up VS Code as a primary dev *and* debug environment on Windows, for local development.

I do not have containers involved in my codebase, but someone could expand on this documentation and provide
extra examples for containers and Linux scenarios.

To start, so far, it's taken me several extensions to assemble Voltron - so to speak.
___

I recommend using [Strawberry Perl](https://strawberryperl.com/) - simply because it's free - and I have had no issues with it thus far.

I am currently on version 5.26.1.1. with modern Strawberry Perl, you may not need to install extra libraries.  I needed to install the following on this version:

- cpan install Perl::LanguageServer
- cpan install PadWalker
___

I would recommend grabbing the following four VS Code Perl Extensions:

- [Perl](https://marketplace.visualstudio.com/items?itemName=richterger.perl)
- [Perl Toolbox](https://marketplace.visualstudio.com/items?itemName=d9705996.perl-toolbox)
- [Perl Navigator](https://marketplace.visualstudio.com/items?itemName=bscan.perlnavigator)
- [Perl Debug Adaptor](https://marketplace.visualstudio.com/items?itemName=Nihilus118.perl-debugger)

At this point you can view the launch.json file to see the various configs I've got, I tried to name them for the various scenarios, you should be able to match the launch configurations to the 3 test files I created to show argument consumption, but I will explicitly map them here:
___

|launch.json Config    | Perl call                     | Test File            |
|:--------------------:|:-----------------------------:|:--------------------:|
|Perl Debug - No Args  | perl {script}.pl              | test.pl              |
|Perl Debug - Raw Args | perl {script}.pl abc          | testWithArgs.pl      |
|Perl Debug - perl -s  | perl -s {script}.pl -test=abc | testWithDashSArgs.pl |

Note that with the perl -s equivalent, one must place `#!/usr/bin/perl -s` at the top of the file in order to allow that behavior with the way the Perl extensions actually call Perl.

There is a high probability that there are kinks to be worked out, but the only one I've found is that sometimes the @INC statements aren't found - that's a reminder to double check
your working directory.  You can modify the launch.json file with an extra parameter - one I've commented out in each Configuration - which will use the workspace folder that shares a location with the file.  You may also set it to be an explicit directory if all the libs you need outside of the $PATH defaults are in one spot.  Alternatively, you can work to figure out how the @INC statements can potentially be setup and suggest edits to this document.

Please feel free to pose revisions to this documentation as needed.
