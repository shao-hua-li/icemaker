Maker of ICE (Internal Compiler Error).

A small program to automatically find crashes in the rust compiler, clippy, rustdoc, rustfmt and miri.
Runs executable on a vast number of rust files (such as rustcs testsuit or glacier) and filters all the crashes.

Features:
* run rustc, clippy, rustdoc, rustfmt, miri, cg_clif or kani on a file and check if there is a crash
* parallel execution
* check different combinations of RUSTFLAGS
* try to find minimal set of RUSTFLAGS that reproduces the internal compiler error
* check if a file compiles stably with incremental compilation
* build and run a file or tests under miri
* run clippy or rustc on a file and find out if (and which) lint does not apply successfully (causes compiler errors)
* find rustc diagnostics that change the file but do not managed to actually fix the broken code
* use "prlimit" to protect against etenally hanging processes or OOMs during infinite loops
* fuzz incremental compilation by using tree-splicer-rust to cause modifications for incremental compilation testing

Requirements: 
 * by default, we build with the "ci" feature disabled and require "prlimit" to limit memory and runtime of a process

History:  
This project started years ago as a simple bash oneliner like  
````
for file in `find . | grep \.rs$` ;do ; echo $file; clippy-driver $file |& grep panicked ; done 
````
but later I decided to RIIR and add support for rustc, rustdoc, nicer output, finding UB via miri and broken lint suggestions etc...  

Shout-outs and related projects  
https://github.com/jruderman/fuzz-rustc for getting me 80mb of fuzzing code  
https://github.com/dwrensha/fuzz-rustc which I could use to generate more output  
https://github.com/Nilstrieb/cargo-minimize testcase reduction  
https://github.com/langston-barrett/treereduce testcase reducion  
https://github.com/langston-barrett/tree-splicer code mutator which icemaker can use to generate more code  


Trophy case (610+):  
  
https://github.com/rust-lang/rust/issues/112242  
https://github.com/model-checking/kani/issues/2502  
https://github.com/model-checking/kani/issues/2501  
https://github.com/model-checking/kani/issues/2499  
https://github.com/model-checking/kani/issues/2498  
https://github.com/model-checking/kani/issues/2497  
https://github.com/rust-lang/rust-clippy/issues/10874  
https://github.com/rust-lang/rust/issues/112208  
https://github.com/rust-lang/rust/issues/112201  
https://github.com/rust-lang/rust/issues/111883  
https://github.com/rust-lang/rust/issues/111879  
https://github.com/rust-lang/rust/issues/111877  
https://github.com/rust-lang/rust/issues/111828  
https://github.com/rust-lang/rust/issues/111749  
https://github.com/rust-lang/rust/issues/111729  
https://github.com/rust-lang/rust/issues/111727  
https://github.com/rust-lang/rust/issues/111529  
https://github.com/rust-lang/rust/issues/111528  
https://github.com/rust-lang/rust/issues/111522  
https://github.com/rust-lang/rust/issues/111521  
https://github.com/rust-lang/rust/issues/111520  
https://github.com/rust-lang/rust/issues/111515  
https://github.com/rust-lang/rust/issues/111510  
https://github.com/rust-lang/rust/issues/111500  
https://github.com/rust-lang/rustfix/issues/219  
https://github.com/rust-lang/rust/issues/111468  
https://github.com/rust-lang/rust/issues/111433  
https://github.com/rust-lang/rust/issues/111418  
https://github.com/rust-lang/rust/issues/111417  
https://github.com/rust-lang/rust/issues/111416  
https://github.com/rust-lang/rust/issues/111411  
https://github.com/rust-lang/rust/issues/111404  
https://github.com/rust-lang/rust/issues/111400  
https://github.com/rust-lang/rust/issues/111399  
https://github.com/rust-lang/rust/issues/111397  
https://github.com/rust-lang/rust/issues/111390  
https://github.com/rust-lang/rust/issues/111341  
https://github.com/rust-lang/rust-clippy/issues/10756  
https://github.com/rust-lang/rust-clippy/issues/10755  
https://github.com/rust-lang/rust/issues/111280  
https://github.com/rust-lang/rust/issues/111232  
https://github.com/rust-lang/rust/issues/111216  
https://github.com/rust-lang/rust/issues/111214  
https://github.com/rust-lang/rust/issues/111206  
https://github.com/rust-lang/rust/issues/111205  
https://github.com/rust-lang/rust/issues/111185  
https://github.com/rust-lang/rust/issues/111184  
https://github.com/rust-lang/rust/issues/111176  
https://github.com/rust-lang/rust/issues/111051  
https://github.com/rust-lang/rust/issues/110969  
https://github.com/rust-lang/miri/issues/2861  
https://github.com/rust-lang/rust/issues/110941  
https://github.com/rust-lang/rust/issues/110929  
https://github.com/rust-lang/rust/issues/110900  
https://github.com/rust-lang/rust/issues/110899  
https://github.com/rust-lang/rust/issues/110892  
https://github.com/rust-lang/rust/issues/110887  
https://github.com/rust-lang/rust/issues/110858  
https://github.com/rust-lang/rust/issues/110781  
https://github.com/rust-lang/rust/issues/110771  
https://github.com/rust-lang/rust/issues/110745  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1370  
https://github.com/rust-lang/rust/issues/110741  
https://github.com/rust-lang/rust/issues/110740  
https://github.com/rust-lang/rust/issues/110723  
https://github.com/rust-lang/rust/issues/110696  
https://github.com/rust-lang/rust/issues/110687  
https://github.com/rust-lang/rust/issues/110683  
https://github.com/rust-lang/rust/issues/110630  
https://github.com/rust-lang/rust/issues/110629  
https://github.com/rust-lang/miri/issues/2847  
https://github.com/rust-lang/rust/issues/110561  
https://github.com/rust-lang/rust/issues/110557  
https://github.com/rust-lang/rust/issues/110549  
https://github.com/rust-lang/rust/issues/110547  
https://github.com/rust-lang/rust/issues/110467  
https://github.com/rust-lang/rust/issues/110464  
https://github.com/rust-lang/rust-clippy/issues/10645  
https://github.com/rust-lang/rust/issues/110206  
https://github.com/rust-lang/rust-clippy/issues/10633  
https://github.com/rust-lang/rust/issues/110164  
https://github.com/rust-lang/rust/issues/110161  
https://github.com/rust-lang/rust/issues/110157  
https://github.com/rust-lang/rust/issues/110138  
https://github.com/rust-lang/rust/issues/110052  
https://github.com/rust-lang/rust/issues/110005  
https://github.com/rust-lang/rust/issues/109992  
https://github.com/rust-lang/rustfmt/issues/5735  
https://github.com/rust-lang/rust/issues/109898  
https://github.com/rust-lang/rustfmt/issues/5734  
https://github.com/rust-lang/rust/issues/109854  
https://github.com/rust-lang/rust/issues/109853  
https://github.com/rust-lang/rust/issues/109832  
https://github.com/rust-lang/rust/issues/109831  
https://github.com/rust-lang/rust/issues/109812  
https://github.com/rust-lang/rustfmt/issues/5730  
https://github.com/rust-lang/rustfmt/issues/5729  
https://github.com/rust-lang/rustfmt/issues/5728  
https://github.com/rust-lang/rust/issues/109768  
https://github.com/rust-lang/rust-clippy/issues/10569  
https://github.com/rust-lang/rust/issues/109681  
https://github.com/rust-lang/rust-clippy/issues/10549  
https://github.com/rust-lang/rust-clippy/issues/10548  
https://github.com/rust-lang/rust-clippy/issues/10547  
https://github.com/langston-barrett/tree-splicer/issues/11  
https://github.com/rust-lang/rust/issues/109514  
https://github.com/rust-lang/rust/issues/109396  
https://github.com/rust-lang/rust/issues/109343  
https://github.com/rust-lang/rust/issues/109305  
https://github.com/rust-lang/rust/issues/109304  
https://github.com/rust-lang/rust/issues/109300  
https://github.com/rust-lang/rust/issues/109299  
https://github.com/rust-lang/rust/issues/109298  
https://github.com/rust-lang/rust/issues/109297  
https://github.com/rust-lang/rust/issues/109296  
https://github.com/rust-lang/rust-clippy/issues/10517  
https://github.com/rust-lang/rustfmt/issues/5716  
https://github.com/rust-lang/rust/issues/109239  
https://github.com/rust-lang/rust/issues/109232  
https://github.com/rust-lang/rust/issues/109204  
https://github.com/rust-lang/rust/issues/109191  
https://github.com/rust-lang/rust/issues/109188  
https://github.com/rust-lang/rust/issues/109178  
https://github.com/rust-lang/rust-clippy/issues/10508  
https://github.com/rust-lang/rust/issues/109152  
https://github.com/rust-lang/rust/issues/109148  
https://github.com/rust-lang/rust/issues/109147  
https://github.com/rust-lang/rust/issues/109146  
https://github.com/rust-lang/rust/issues/109144  
https://github.com/rust-lang/rust/issues/109141  
https://github.com/langston-barrett/tree-splicer/issues/7  
https://github.com/rust-lang/rust/issues/109098  
https://github.com/rust-lang/rust/issues/109096  
https://github.com/rust-lang/rust/issues/109090  
https://github.com/rust-lang/rust/issues/109072  
https://github.com/rust-lang/rust/issues/109071  
https://github.com/rust-lang/rust-clippy/issues/10495  
https://github.com/rust-lang/rust/issues/109023  
https://github.com/rust-lang/rust/issues/108957  
https://github.com/rust-lang/rust/issues/108781  
https://github.com/rust-lang/rust-clippy/issues/10452  
https://github.com/rust-lang/rust-clippy/issues/10451  
https://github.com/rust-lang/rust-clippy/issues/10450  
https://github.com/rust-lang/rust-clippy/issues/10449  
https://github.com/rust-lang/rust-clippy/issues/10447  
https://github.com/rust-lang/rust-clippy/issues/10446  
https://github.com/rust-lang/rust/issues/108748  
https://github.com/rust-lang/rust/issues/108742  
https://github.com/rust-lang/rust/issues/108738  
https://github.com/model-checking/kani/issues/2266  
https://github.com/model-checking/kani/issues/2265  
https://github.com/model-checking/kani/issues/2264  
https://github.com/rust-lang/rust/issues/108697  
https://github.com/model-checking/kani/issues/2262  
https://github.com/model-checking/kani/issues/2261  
https://github.com/model-checking/kani/issues/2260  
https://github.com/model-checking/kani/issues/2259  
https://github.com/model-checking/kani/issues/2258  
https://github.com/model-checking/kani/issues/2256  
https://github.com/model-checking/kani/issues/2255  
https://github.com/model-checking/kani/issues/2254  
https://github.com/model-checking/kani/issues/2253  
https://github.com/model-checking/kani/issues/2252  
https://github.com/rust-lang/rust/issues/108529  
https://github.com/rust-lang/rust-clippy/issues/10412  
https://github.com/rust-lang/rust-clippy/issues/10409  
https://github.com/model-checking/kani/issues/2242  
https://github.com/model-checking/kani/issues/2241  
https://github.com/model-checking/kani/issues/2240  
https://github.com/model-checking/kani/issues/2239  
https://github.com/model-checking/kani/issues/2238  
https://github.com/model-checking/kani/issues/2237  
https://github.com/model-checking/kani/issues/2236  
https://github.com/rust-lang/rust/issues/108399  
https://github.com/rust-lang/rust/issues/108266  
https://github.com/rust-lang/rust/issues/108249  
https://github.com/rust-lang/rust/issues/108248  
https://github.com/rust-lang/rust-clippy/issues/10379  
https://github.com/rust-lang/rust-clippy/issues/10374  
https://github.com/rust-lang/rust/issues/108225  
https://github.com/rust-lang/rust/issues/108194  
https://github.com/rust-lang/rust/issues/108192  
https://github.com/rust-lang/rust/issues/108191  
https://github.com/rust-lang/rust/issues/108190  
https://github.com/rust-lang/rust/issues/108184  
https://github.com/rust-lang/rust/issues/108182  
https://github.com/rust-lang/rust/issues/108181  
https://github.com/rust-lang/rust/issues/108180  
https://github.com/rust-lang/rust/issues/108179  
https://github.com/rust-lang/rust/issues/108165  
https://github.com/rust-lang/rust/issues/108158  
https://github.com/rust-lang/rust/issues/107998  
https://github.com/rust-lang/rust/issues/107988  
https://github.com/rust-lang/rust/pull/107973  
https://github.com/rust-lang/rust/pull/107972  
https://github.com/rust-lang/rust/issues/107872  
https://github.com/rust-lang/rust/issues/107860  
https://github.com/rust-lang/rust/issues/107818  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1354  
https://github.com/rust-lang/rust/issues/107705  
https://github.com/rust-lang/rust/issues/107428  
https://github.com/rust-lang/rust/issues/107423  
https://github.com/rust-lang/rust/issues/107414  
https://github.com/rust-lang/rust/issues/107346  
https://github.com/rust-lang/rust/issues/107147  
https://github.com/rust-lang/rust/issues/107093  
https://github.com/rust-lang/rust/issues/107090  
https://github.com/rust-lang/rust/issues/107089  
https://github.com/rust-lang/rust/issues/107088  
https://github.com/rust-lang/rust/issues/107087  
https://github.com/rust-lang/rust/issues/106926  
https://github.com/rust-lang/rust/issues/106882  
https://github.com/rust-lang/rust/issues/106881  
https://github.com/rust-lang/rust/issues/106876  
https://github.com/rust-lang/rust/issues/106862  
https://github.com/rust-lang/rust/issues/106861  
https://github.com/rust-lang/rust/issues/106858  
https://github.com/rust-lang/rust/issues/106857  
https://github.com/rust-lang/rust/issues/106843  
https://github.com/rust-lang/rust/issues/106841  
https://github.com/rust-lang/rust/issues/106755  
https://github.com/rust-lang/rust/issues/106695  
https://github.com/rust-lang/rust/issues/106666  
https://github.com/rust-lang/rust/issues/106226  
https://github.com/rust-lang/rust/issues/106213  
https://github.com/rust-lang/rust/issues/106079  
https://github.com/rust-lang/rust/issues/106030  
https://github.com/rust-lang/rust/issues/105981  
https://github.com/rust-lang/miri/issues/2735  
https://github.com/rust-lang/miri/issues/2734  
https://github.com/rust-lang/rust/issues/105969  
https://github.com/rust-lang/rust/issues/105968  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1330  
https://github.com/rust-lang/rust/issues/105946  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1329  
https://github.com/rust-lang/rust/issues/105937  
https://github.com/rust-lang/rust/issues/105896  
https://github.com/rust-lang/rust/issues/105819  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1327  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1326  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1325  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1324  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1323  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1322  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1321  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1320  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1319  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1317  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1316  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1315  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1313  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1312  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1311  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1310  
https://github.com/rust-lang/rust/issues/105742  
https://github.com/rust-lang/rust/issues/105737  
https://github.com/rust-lang/rust/issues/105709  
https://github.com/rust-lang/rust/issues/105689  
https://github.com/rust-lang/rust/issues/105631  
https://github.com/rust-lang/rust/issues/105591  
https://github.com/rust-lang/rust/issues/105449  
https://github.com/rust-lang/rust/issues/105404  
https://github.com/rust-lang/rust-clippy/issues/10044  
https://github.com/rust-lang/rustfmt/issues/5626  
https://github.com/rust-lang/rust/issues/105334  
https://github.com/rust-lang/rust/issues/105330  
https://github.com/rust-lang/rust/issues/105304  
https://github.com/rust-lang/rust/issues/105288  
https://github.com/rust-lang/rustfmt/issues/5625  
https://github.com/rust-lang/rust/issues/105275  
https://github.com/rust-lang/rust/issues/105273  
https://github.com/rust-lang/rust/issues/105269  
https://github.com/rust-lang/rust/issues/105263  
https://github.com/rust-lang/rust/issues/105260  
https://github.com/rust-lang/rust/issues/105257  
https://github.com/rust-lang/rust/issues/105249  
https://github.com/rust-lang/rust/issues/105232  
https://github.com/rust-lang/rust/issues/105210  
https://github.com/rust-lang/rust/issues/105209  
https://github.com/rust-lang/rust/issues/105202  
https://github.com/rust-lang/rust/issues/105199  
https://github.com/rust-lang/rust/issues/105169  
https://github.com/rust-lang/rust/issues/105150  
https://github.com/rust-lang/rust/issues/105149  
https://github.com/rust-lang/rust/issues/105148  
https://github.com/rust-lang/rust-clippy/issues/10019  
https://github.com/rust-lang/rust-clippy/issues/10018  
https://github.com/rust-lang/rust-clippy/issues/10017  
https://github.com/rust-lang/rust-clippy/issues/10016  
https://github.com/rust-lang/rust-clippy/issues/10015  
https://github.com/rust-lang/rust-clippy/issues/10014  
https://github.com/rust-lang/rust/issues/105099  
https://github.com/rust-lang/rust-clippy/issues/10002  
https://github.com/rust-lang/rust-clippy/issues/10000  
https://github.com/rust-lang/rust/issues/105031  
https://github.com/rust-lang/rust-clippy/issues/9976  
https://github.com/rust-lang/rust/issues/105028  
https://github.com/rust-lang/rust-clippy/issues/9973  
https://github.com/rust-lang/rust-clippy/issues/9961  
https://github.com/rust-lang/rust-clippy/issues/9960  
https://github.com/rust-lang/rust/issues/104918  
https://github.com/rust-lang/rust-clippy/issues/9957  
https://github.com/rust-lang/rust-clippy/issues/9956  
https://github.com/rust-lang/rust-clippy/issues/9955  
https://github.com/rust-lang/rust-clippy/issues/9954  
https://github.com/rust-lang/rust-clippy/issues/9953  
https://github.com/rust-lang/rust-clippy/issues/9952  
https://github.com/rust-lang/rust-clippy/issues/9951  
https://github.com/rust-lang/rust-clippy/issues/9949  
https://github.com/rust-lang/rust/issues/104913  
https://github.com/rust-lang/rust-clippy/issues/9947  
https://github.com/rust-lang/rust/issues/104910  
https://github.com/rust-lang/rust-clippy/issues/9946  
https://github.com/rust-lang/rust/issues/104904  
https://github.com/rust-lang/rust/issues/104897  
https://github.com/rust-lang/rust-clippy/issues/9942  
https://github.com/rust-lang/rust/issues/104870  
https://github.com/rust-lang/rust-clippy/issues/9935  
https://github.com/rust-lang/rust/issues/104817  
https://github.com/rust-lang/rust/issues/104794  
https://github.com/rust-lang/rust/issues/104695  
https://github.com/rust-lang/rust-clippy/issues/9917  
https://github.com/rust-lang/rust-clippy/issues/9916  
https://github.com/rust-lang/rust-clippy/issues/9915  
https://github.com/rust-lang/rust-clippy/issues/9914  
https://github.com/rust-lang/rust-clippy/issues/9913  
https://github.com/rust-lang/rust-clippy/issues/9912  
https://github.com/rust-lang/rust-clippy/issues/9911  
https://github.com/rust-lang/rust-clippy/issues/9910  
https://github.com/rust-lang/rust-clippy/issues/9909  
https://github.com/rust-lang/rust-clippy/issues/9908  
https://github.com/rust-lang/rust-clippy/issues/9907  
https://github.com/rust-lang/rust-clippy/issues/9906  
https://github.com/rust-lang/rust-clippy/issues/9905  
https://github.com/rust-lang/rust-clippy/issues/9904  
https://github.com/rust-lang/rust-clippy/issues/9903  
https://github.com/rust-lang/rust-clippy/issues/9902  
https://github.com/rust-lang/rust-clippy/issues/9901  
https://github.com/rust-lang/rust-clippy/issues/9900  
https://github.com/rust-lang/rust-clippy/issues/9899  
https://github.com/rust-lang/rust-clippy/issues/9898  
https://github.com/rust-lang/rust-clippy/issues/9897  
https://github.com/rust-lang/rust-clippy/issues/9896  
https://github.com/rust-lang/rust-clippy/issues/9895  
https://github.com/rust-lang/rust-clippy/issues/9894  
https://github.com/rust-lang/rust-clippy/issues/9893  
https://github.com/rust-lang/rust-clippy/issues/9892  
https://github.com/rust-lang/rust-clippy/issues/9891  
https://github.com/rust-lang/rust-clippy/issues/9890  
https://github.com/rust-lang/rust-clippy/issues/9889  
https://github.com/rust-lang/rust/issues/104631  
https://github.com/rust-lang/rust-clippy/issues/9888  
https://github.com/rust-lang/rust-clippy/issues/9887  
https://github.com/rust-lang/rust-clippy/issues/9886  
https://github.com/rust-lang/rust-clippy/issues/9885  
https://github.com/rust-lang/rust-clippy/issues/9884  
https://github.com/rust-lang/rust-clippy/issues/9883  
https://github.com/rust-lang/rust-clippy/issues/9882  
https://github.com/rust-lang/rust-clippy/issues/9866  
https://github.com/rust-lang/rust/issues/104518  
https://github.com/rust-lang/rust/issues/104440  
https://github.com/rust-lang/rust/issues/104432  
https://github.com/rust-lang/rust/issues/104392  
https://github.com/rust-lang/rust/issues/104237  
https://github.com/rust-lang/rust/issues/104173  
https://github.com/rust-lang/rust/issues/104085  
https://github.com/rust-lang/rust/issues/104040  
https://github.com/rust-lang/rust/issues/104037  
https://github.com/rust-lang/rust/issues/103679  
https://github.com/rust-lang/rust/issues/102989  
https://github.com/rust-lang/rust/issues/102986  
https://github.com/rust-lang/rust/issues/102985  
https://github.com/rust-lang/rust/issues/102946  
https://github.com/rust-lang/rust/issues/102933  
https://github.com/rust-lang/rust/issues/102827  
https://github.com/rust-lang/rust/issues/102828  
https://github.com/rust-lang/rust/issues/102796  
https://github.com/rust-lang/rust/issues/102768  
https://github.com/rust-lang/rust/issues/102645  
https://github.com/rust-lang/rust/issues/102571  
https://github.com/rust-lang/rust/issues/102467  
https://github.com/rust-lang/rust/issues/102465  
https://github.com/rust-lang/rust/issues/102363  
https://github.com/rust-lang/rust/issues/102156  
https://github.com/rust-lang/rust/issues/102154  
https://github.com/rust-lang/rust/issues/102124  
https://github.com/rust-lang/rust/issues/102105  
https://github.com/rust-lang/rust/issues/101964  
https://github.com/rust-lang/rust/issues/101962  
https://github.com/rust-lang/rust/issues/101739  
https://github.com/rust-lang/rust-clippy/issues/9463  
https://github.com/rust-lang/rust-clippy/issues/9459  
https://github.com/rust-lang/rust-clippy/issues/9433  
https://github.com/rust-lang/rust/issues/101517  
https://github.com/rust-lang/rust/issues/101505  
https://github.com/rust-lang/rust/issues/101243  
https://github.com/rust-lang/rust/issues/101113  
https://github.com/rust-lang/rust/issues/101076  
https://github.com/rust-lang/rust/issues/100948  
https://github.com/rust-lang/miri/issues/2499  
https://github.com/rust-lang/rust/issues/100783  
https://github.com/rust-lang/rust/issues/100778  
https://github.com/rust-lang/rust/issues/100772  
https://github.com/rust-lang/rust/issues/100770  
https://github.com/rust-lang/miri/issues/2496  
https://github.com/rust-lang/rust/issues/100612  
https://github.com/rust-lang/rust/issues/100485  
https://github.com/rust-lang/rust/issues/100484  
https://github.com/rust-lang/rust/issues/100191  
https://github.com/rust-lang/rust/issues/100187  
https://github.com/rust-lang/rust/issues/100154  
https://github.com/rust-lang/rust/issues/100047  
https://github.com/rust-lang/rust/issues/99876  
https://github.com/rust-lang/rust/issues/99820  
https://github.com/rust-lang/miri/issues/2433  
https://github.com/rust-lang/miri/issues/2432  
https://github.com/rust-lang/rust/issues/99662  
https://github.com/rust-lang/rust/issues/99647  
https://github.com/rust-lang/rust/issues/99387  
https://github.com/rust-lang/rust/issues/99363  
https://github.com/rust-lang/rust/issues/99331  
https://github.com/rust-lang/rust/issues/99325  
https://github.com/rust-lang/rust/issues/99319  
https://github.com/rust-lang/rust/issues/99318  
https://github.com/rust-lang/rust/issues/99228  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1244  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1243  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1242  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1241  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1240  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1239  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1238  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1237  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1236  
https://github.com/bjorn3/rustc_codegen_cranelift/issues/1235  
https://github.com/rust-lang/miri/issues/2340  
https://github.com/rust-lang/rust/issues/98821  
https://github.com/rust-lang/rust/issues/98372  
https://github.com/rust-lang/rust/issues/98250  
https://github.com/rust-lang/rust/issues/98171  
https://github.com/rust-lang/miri/issues/2234  
https://github.com/rust-lang/rust/issues/98016  
https://github.com/rust-lang/rust/issues/98009  
https://github.com/rust-lang/rust/issues/98007  
https://github.com/rust-lang/rust/issues/98006  
https://github.com/rust-lang/rust/issues/98003  
https://github.com/rust-lang/rust/issues/98002  
https://github.com/rust-lang/rust/issues/97728  
https://github.com/rust-lang/rust/issues/97726  
https://github.com/rust-lang/rust/issues/97725  
https://github.com/rust-lang/rust/issues/97698  
https://github.com/rust-lang/rust/issues/97695  
https://github.com/rust-lang/rust/issues/97270  
https://github.com/rust-lang/rust/issues/97194  
https://github.com/rust-lang/rust/issues/97193  
https://github.com/rust-lang/rust/issues/97049  
https://github.com/rust-lang/rust/issues/97006  
https://github.com/rust-lang/miri/issues/2106  
https://github.com/rust-lang/miri/issues/2088  
https://github.com/rust-lang/rust/issues/96765  
https://github.com/rust-lang/rust/issues/96767  
https://github.com/rust-lang/rust/issues/96721  
https://github.com/rust-lang/rust/issues/96485  
https://github.com/rust-lang/rust/issues/96395  
https://github.com/rust-lang/rust-clippy/issues/8748  
https://github.com/rust-lang/rust/issues/96381  
https://github.com/rust-lang/rust/issues/96288  
https://github.com/rust-lang/rust/issues/96287  
https://github.com/rust-lang/rust/issues/96200  
https://github.com/rust-lang/rust/issues/96191  
https://github.com/rust-lang/rust/issues/96185  
https://github.com/rust-lang/rust/issues/96175  
https://github.com/rust-lang/rust/issues/96172  
https://github.com/rust-lang/rust/issues/96170  
https://github.com/rust-lang/rust/issues/96169  
https://github.com/rust-lang/rust/issues/96114  
https://github.com/rust-lang/rust/issues/95978  
https://github.com/rust-lang/rust/issues/95879  
https://github.com/rust-lang/rust/issues/95878  
https://github.com/rust-lang/rust/issues/95640  
https://github.com/rust-lang/rust/issues/95327  
https://github.com/rust-lang/rust/issues/95307  
https://github.com/rust-lang/rust/issues/95163  
https://github.com/rust-lang/rust/issues/95128  
https://github.com/rust-lang/rust/issues/95023  
https://github.com/rust-lang/rust/issues/94961  
https://github.com/rust-lang/rust/issues/94953  
https://github.com/rust-lang/rust/issues/94903  
https://github.com/rust-lang/rust/issues/94822  
https://github.com/rust-lang/rust/issues/94725  
https://github.com/rust-lang/rust/issues/94654  
https://github.com/rust-lang/rust/issues/94629  
https://github.com/rust-lang/rust/issues/94627  
https://github.com/rust-lang/rust/issues/94516  
https://github.com/rust-lang/rust/issues/94382  
https://github.com/rust-lang/rust/issues/94380  
https://github.com/rust-lang/rust/issues/94379  
https://github.com/rust-lang/rust/issues/94378  
https://github.com/rust-lang/rust/issues/94171  
https://github.com/rust-lang/rust/issues/94149  
https://github.com/rust-lang/rust/issues/94073  
https://github.com/rust-lang/rust/issues/93871  
https://github.com/rust-lang/rust/issues/93788  
https://github.com/rust-lang/rust/issues/93688  
https://github.com/rust-lang/rust/issues/93578  
https://github.com/rust-lang/rust/issues/93117  
https://github.com/rust-lang/rust-clippy/issues/8245  
https://github.com/rust-lang/rust-clippy/issues/8244  
https://github.com/rust-lang/rust/issues/92495  
https://github.com/rust-lang/rust/issues/92240  
https://github.com/rust-lang/rust/issues/91745  
https://github.com/rust-lang/rust/issues/90192  
https://github.com/rust-lang/rust/issues/90191  
https://github.com/rust-lang/rust/issues/90189  
https://github.com/rust-lang/rust/issues/89312  
https://github.com/rust-lang/rust/issues/89271  
https://github.com/rust-lang/rust/issues/89066  
https://github.com/rust-lang/rust/issues/88536  
https://github.com/rust-lang/rustfmt/issues/4968  
https://github.com/rust-lang/rust/issues/88434  
https://github.com/rust-lang/rust/issues/88433  
https://github.com/rust-lang/rust/issues/88171  
https://github.com/rust-lang/rust/issues/87563  
https://github.com/rust-lang/rust/issues/87308  
https://github.com/rust-lang/rust/issues/87219  
https://github.com/rust-lang/rust/issues/87218  
https://github.com/rust-lang/rust/issues/85871  
https://github.com/rust-lang/rust/issues/85552  
https://github.com/rust-lang/rust/issues/85480  
https://github.com/rust-lang/rust/issues/83921  
https://github.com/rust-lang/rust/issues/83190  
https://github.com/rust-lang/rust/issues/83048  
https://github.com/rust-lang/rust/issues/82678  
https://github.com/rust-lang/rust/issues/82329  
https://github.com/rust-lang/rust/issues/82328  
https://github.com/rust-lang/rust/issues/82327  
https://github.com/rust-lang/rust/issues/82326  
https://github.com/rust-lang/rust/issues/82325  
https://github.com/rust-lang/rust/issues/81627  
https://github.com/rust-lang/rust/issues/81403  
https://github.com/rust-lang/rust/issues/80589  
https://github.com/rust-lang/rust/issues/80251  
https://github.com/rust-lang/rust/issues/80231  
https://github.com/rust-lang/rust/issues/80230  
https://github.com/rust-lang/rust/issues/80229  
https://github.com/rust-lang/rust/issues/80228  
https://github.com/rust-lang/rust/issues/80060  
https://github.com/rust-lang/rustfmt/issues/4587  
https://github.com/rust-lang/rustfmt/issues/4586  
https://github.com/rust-lang/rust/issues/79699  
https://github.com/rust-lang/rust/issues/79669  
https://github.com/rust-lang/rust/issues/79569  
https://github.com/rust-lang/rust/issues/79566  
https://github.com/rust-lang/rust/issues/79565  
https://github.com/rust-lang/rust/issues/79497  
https://github.com/rust-lang/rust/issues/79496  
https://github.com/rust-lang/rust/issues/79495  
https://github.com/rust-lang/rust/issues/79494  
https://github.com/rust-lang/rust/issues/79468  
https://github.com/rust-lang/rust/issues/79467  
https://github.com/rust-lang/rust/issues/79466  
https://github.com/rust-lang/rust/issues/79465  
https://github.com/rust-lang/rust/issues/79461  
https://github.com/rust-lang/rust/issues/79099  
https://github.com/rust-lang/rust/issues/79066  
https://github.com/rust-lang/rust/issues/78628  
https://github.com/rust-lang/rust/issues/78560  
https://github.com/rust-lang/rust/issues/78520  
https://github.com/rust-lang/rust/issues/78510  
https://github.com/rust-lang/rust/issues/78442  
https://github.com/rust-lang/rust/issues/78441  
https://github.com/rust-lang/rust/issues/78233  
https://github.com/rust-lang/rust/issues/78180  
https://github.com/rust-lang/rust/issues/77669  
https://github.com/rust-lang/rust/issues/77668  
https://github.com/rust-lang/rust/issues/75962  
https://github.com/rust-lang/rust/issues/75507  
https://github.com/rust-lang/rust/issues/75506  
https://github.com/rust-lang/rust/issues/75053  
https://github.com/rust-lang/rust/issues/75051  
https://github.com/rust-lang/rust/issues/73860  
https://github.com/rust-lang/rust/issues/74358  
https://github.com/rust-lang/rust/issues/73260  
https://github.com/rust-lang/rust/issues/73022  
https://github.com/rust-lang/rust/issues/73021  
https://github.com/rust-lang/rust/issues/73020  
https://github.com/rust-lang/rust/issues/72960  
https://github.com/rust-lang/rust/issues/72911  
https://github.com/rust-lang/rust/issues/72679  
https://github.com/rust-lang/rust/issues/72285  
https://github.com/rust-lang/rust/issues/72181  
https://github.com/rust-lang/rust/issues/72105  
https://github.com/rust-lang/rust/issues/69875  
https://github.com/rust-lang/rust/issues/69416  
https://github.com/rust-lang/rust/issues/69415  
https://github.com/rust-lang/rust/issues/69409  
https://github.com/rust-lang/rust/issues/69414  
https://github.com/rust-lang/rust/issues/69398  
https://github.com/rust-lang/rust/issues/68750  
https://github.com/rust-lang/rust/issues/68749  
https://github.com/rust-lang/rust/issues/68296  
https://github.com/rust-lang/rust/issues/67696  
https://github.com/rust-lang/rust/issues/67641  
https://github.com/rust-lang/rust/issues/67640  
https://github.com/rust-lang/rust/issues/67639  
https://github.com/rust-lang/rust/issues/67550  

#### License:

Copyright 2020-2023 Matthias Krüger

````
Licensed under the Apache License, Version 2.0 <LICENSE-APACHE or
http://www.apache.org/licenses/LICENSE-2.0> or the MIT license
<LICENSE-MIT or http://opensource.org/licenses/MIT>, at your
option. All files in the project carrying such notice may not be
copied, modified, or distributed except according to those terms.
````
