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

sub checkYn { ## provided a prompt, will ask user how to proceed, assuming YES and else opting yes
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

```
