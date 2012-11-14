dnscmp
======

DNS server comparison, query by uery

Usage: dnscmp host1:port host2:port testsfile

dnscmp sends queries defined in the tests file to two DNS servers and
compares their results.  Results may be compared on just the answer
section or on query flags.  Certain RR types will be compared in specific
ways (e.g., SOA sections, etc.).  If more than one RR is returned, they
are sorted first and then compared.  Any standard DNS header flag may
be used in the comparison.

Test file format:

queryname TYPE answer flag:xx flag:xx

www.google.com A answer flag:rd flag:ra
yahoo.com MX answer
mail.yahoo.com CNAME answer flag:ra
mozilla.org DNSKEY answer flag:ad
1.1.80.10.in-addr.arpa PTR answer

notes
=====

dnscmp is designed to be used in testing and verifying DNS server
configurations where the operational aspects can be compared with a
known good server (e.g., when you are restructuring a configuration
file or making changes to other zones).  It is not designed to test
a running name server against zone files or other "model" behavior
that is not itself a running name server.  dnscmp is designed to
primarily test queries and servers that are under your direct control.

Also note that when comparing two name servers answers may differ
in known ways - e.g., based on geographic or network location when
anycast DNS is in use, or when customized zone files are otherwise
provided to different name servers.  This may be particularly true
when issuing queries for certain large internet search engines, for
example.

