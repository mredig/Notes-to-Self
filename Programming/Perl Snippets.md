<!-- permalink: 5de0dee00c4ff6c42f920f7b9c63b166 DO NOT DELETE OR EDIT THIS LINE -->
# Perl Snippets

This is a collection of Perl snippets I've written or otherwise come across that I would like available for future reference.

### Prints contents of a file
```
sub showFileContents {
	my $file = $_[0];
	open FILE, "<$file";
	my @hold = <FILE>;
	foreach(@hold) {
		print $_;
	}
	close FILE;
}
```

### clears screen and then prints provided string
```
sub printHeader {
	my $header = $_[0];
	&runOnSystem("clear");
	print "\n\n\t$header:\n\n";
}
```

### executes system command and communicates to user what it's doing - be sure to be careful of arbitrary code execution
```
sub runOnSystem {
	my $command = $_[0];
	my $debug = $_[1];
	if ($debug) {
		print "debug: $command\n";
	} else {
		print "\n\n[[executing: $command]]\n\n";
		system("$command");
	}
}
```

### prompts user to press enter to continue
```
sub enterToContinue {
	print "\nPress enter to continue...\n";
	my $enter = <STDIN>;
}
```

### provided a prompt, will ask user how to proceed, assuming YES and else opting no
```
sub checkYn {
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
```

### provided a prompt, will ask user how to proceed, assuming NO and else opting yes
```
sub checkyN {
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
```

### gets the directory of the currently running script. note requirement
```
sub getExecutableDirectory {
	## requires use Cwd 'abs_path';
	my $fullPath = abs_path($0);
	my $dirname  = dirname($fullPath);
	return $dirname;
}
```

### template for getting a timestamp string
```
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
```

### process arguments provided from command line
this one is a bit more specific, but should be easily adaptable
```
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
		print "Usage: example usage\n";
	}

}
sub processArgument {
	my $arg = $_[0];
	my $nextArg = $_[1];
	if ($arg eq "c" && $nextArg ne "") { #maybe do -e
		# most of these are examples as to how to use this code
		# my $confFile = $nextArg;
		# &loadConfFile($confFile);
	} elsif ($arg eq "d") {
		#$debug = 1;
	}
}
```

### check for a trailing slash in a string
```
sub checkTrailingSlash {
	my $str = $_[0];
	if ($str !~ /\/$/) {
		$str .= "/";
	}
	return $str;
}

```
