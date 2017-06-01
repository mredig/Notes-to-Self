# Perl Snippets

This is a collection of Perl snippets I've written or otherwise come across that I would like available for future reference.

```

sub showFileContents { ## Prints contents of a file
	my $file = $_[0];
	open FILE, "<$file";
	my @hold = <FILE>;
	foreach(@hold) {
		print $_;
	}
	close FILE;
}

sub printHeader { ## clears screen and then prints provided string
	my $header = $_[0];
	&runOnSystem("clear");
	print "\n\n\t$header:\n\n";
}

sub runOnSystem { ## executes system command and communicates to user what it's doing - be sure to be careful of arbitrary code execution
	my $command = $_[0];
	my $debug = $_[1];
	if ($debug) {
		print "debug: $command\n";
	} else {
		print "\n\n[[executing: $command]]\n\n";
		system("$command");
	}
}

sub enterToContinue {
	print "\nPress enter to continue...\n";
	my $enter = <STDIN>;
}

sub checkYn { ## provided a prompt, will ask user how to proceed, assuming YES and else opting no
	my $prompt = $_[0] . " [Y/n]:";
	print "$prompt";
	my $rVal = -1;
	while($rVal == -1) {
		chomp(my $yn = <STDIN>);
		if ($yn =~ /^y*$/i) {
		 	$rVal = 1;
		} elsif ($yn =~ /^n+$/i) {
			$rVal = 0;
		} else {
			print "Sorry, that's not valid input. Please try again:\n\n$prompt";
		}
	}
	return $rVal;
}

sub checkyN { ## provided a prompt, will ask user how to proceed, assuming NO and else opting yes
	my $prompt = $_[0] . " [y/N]:";
	print "$prompt";
	my $rVal = -1;
	while($rVal == -1) {
		chomp(my $yn = <STDIN>);
		if ($yn =~ /^y+$/i) {
		 	$rVal = 1;
		} elsif ($yn =~ /^n*$/i) {
			$rVal = 0;
		} else {
			print "Sorry, that's not valid input. Please try again:\n\n$prompt";
		}
	}
	return $rVal;
}

sub getExecutableDirectory {
	## use Cwd 'abs_path';
	## use File::Basename;
	my $fullPath = abs_path($0);
	my $dirname  = dirname($fullPath);
	return $dirname;
}

sub getTimeStampString() {
	($sec,$min,$hour,$mday,$mon,$year,$wday,$yday,$isdst) = localtime(time);

	$year += 1900;
	$mon += 1;
	$mon = sprintf("%02d", $mon);
	$mday = sprintf("%02d", $mday);
	$hour = sprintf("%02d", $hour);
	$min = sprintf("%02d", $min);
	$string = "$year$mon$mday-$hour$min";
	return $string;
}

## this next one is a bit more specific, but should be easily adaptable
sub processArguments {
	$ranSomething = 0;
	for (my $i = 0; $i < scalar(@ARGV); $i++) {
		my $arg = $ARGV[$i];
		if ($arg =~ /^-(\w)/) {
			$arg = $1;
			&processArgument($arg, $ARGV[$i + 1]);
		}
	}
	if ($ranSomething == 0) {
		print "Usage: clam_run_conf -c [pathtoconf1] -c [pathtoconf2]\n\nno limit on conf inputs\nwill DIE on first incorrectly formatted conf - following confs will NOT be run!\n";
	}

}
sub processArgument {
	my $arg = $_[0];
	my $nextArg = $_[1];
	if ($arg eq "c" && $nextArg ne "") { #maybe do -e
		my $confFile = $nextArg;
		my %borgJob = &loadConfFile($confFile);
		&runBorgJob(\%borgJob);
	} elsif ($arg eq "d") {
		$debug = 1;
	}
}

sub checkTrailingSlash {
	my $str = $_[0];
	if ($str !~ /\/$/) {
		$str .= "/";
	}
	return $str;
}

#get current user
my $login = getlogin;


sub convertToUnixLineEndings {
	my $str = $_[0];
	$str =~ s/\r\n/\n/g;
	return $str;
}


```
