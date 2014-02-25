
# github2sprintly

This is a tool to import issues and comments from a single Github repo into a
single project hosted on http://Sprint.ly.

To use it, you'll find to get Github and Sprint.ly API keys, and fill in some
related values in the ./github2sprintly script. Open up that script to see
details.

I recommend you first run it against a test Sprint.ly project-- Make sure that
all team members are also added to this project to avoid import errors.

Once you get the import perfect in the test project in Sprint.ly, you can
delete that project and run it against your actual target project.

## Features

The script runs up to 8x parallel threads by default, to make your import run
faster.

It also detects if Sprint.ly is returning a temporary "502 Bad Gateway"
response. In that case, it tries again until that request goes through.

Debugging output is printed to the screen, and a final summary is reported when
it finishes.  Note that you are watching several tasks happen at once. You will
see a mix of items starting and finishing importing, rather than a single
linear stream of just one item after another.

## Recommended Usage

    # ... Modify github2sprintly according to the comments there, then:

    # install dependencies (run in the project directory)
    npm install

    ./node github2sprintly | tee output.txt

Output will go STDOUT and be written to output.txt as well. You may wish to
have the output as a reference for later.

## Known issues

 * **Pagination is not implemented**. If you have more than 100 open or closed issues, you need to to update this code to support fetching additional pages of issues. Otherwise, issues will be silently dropped.
 * **No max tries for 502 retries**. It could be considered a bug that we will retry indefinitely if Sprint.ly returns a 502. Given up after N tries would be a nice addition to cover the edge case where Sprint.ly is having an ongoing issue.


## Warranty, Support, feature requests and bug reports

There is no warranty, no support and no further improvements planned. Our
one-time import is done.

If you want any changes, you are welcome to fork it and make them, but bug
reports will go un-addressed.

## Author 

Mark Stosberg <mark@rideamigos.com>

## License 

Released as open source software under the BSD License



