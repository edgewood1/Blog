In JavaScript, the URL constructor is used to create URL objects and parse URLs.

Parts of a valid URL:

__Scheme__: A valid URL typically starts with a scheme, such as "http," "https," "ftp," "file," etc. The scheme is followed by a colon and two forward slashes (e.g., "http://").

* two forward slashes are called ....

__Domain or Host__: After the scheme, a valid URL should have a domain or host name. This can be an IP address or a domain name (e.g., "www.example.com" or "192.168.0.1").

__Port__: The URL can **optionally** include a port number after the host, separated by a colon (e.g., "http://example.com:8080").

__Path__: The path is a string that follows the domain and port (if present). It represents the resource or location on the server (e.g., "/path/to/resource").

__Query__: URLs can include a query string, which starts with a question mark and contains key-value pairs (e.g., "?key1=value1&key2=value2").

__Fragment Identifier__: A URL may also include a fragment identifier, which is preceded by a hash symbol (#) and is used to specify a specific section within a web page (e.g., "#section1").

```jsx
const urlString = "https://www.example.com:8080/path/to/resource?key1=value1#section1";
const url = new URL(urlString);

console.log(url.protocol); // Output: "https:"
console.log(url.host); // Output: "www.example.com:8080"
console.log(url.pathname); // Output: "/path/to/resource"
console.log(url.search); // Output: "?key1=value1"
console.log(url.hash); // Output: "#section1"
```

If a URL string adheres to these rules and structures, it is considered valid and can be successfully parsed using the URL constructor in JavaScript. If it does not conform to these rules, creating a URL object may result in an error.


The URL object in JavaScript doesn't come with many methods, but it does have several properties that allow you to access different parts of the URL. Here are the properties:

href: The entire URL.
protocol: The protocol of the URL (e.g., 'http:').
username: The username specified before the domain name.
password: The password specified before the domain name.
host: The hostname and port (if specified) of the URL.
hostname: The domain name of the URL.
port: The port number of the URL.
pathname: The path section of the URL.
search: The query string of the URL, including the leading '?' character.
hash: The fragment identifier of the URL, including the leading '#' character.
origin: The origin of the URL.
The URL object also has a searchParams property, which is a URLSearchParams object that can be used to work with the query string of the URL. The URLSearchParams object has several methods, including:

append(name, value): Appends a new value to an existing key, or adds the key if it does not exist.
delete(name): Deletes the specified key and its associated value(s).
get(name): Returns the first value associated with the given key.
getAll(name): Returns all values associated with the given key.
has(name): Returns a boolean indicating whether the given key exists.
set(name, value): Sets the value associated with a given key to a single value. If the key already exists, its value(s) are replaced.
Note: The URL object is immutable, meaning that its properties cannot be changed after it's created. However, you can create a new URL object with a modified URL by using the URL object's properties to construct a new URL string.