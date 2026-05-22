---
date: 2026-05-22T23:04:58+08:00
source: clipboard
chars: 9540
---

pip3 install litellm
Defaulting to user installation because normal site-packages is not writeable
Collecting litellm
  Downloading litellm-1.83.9-py3-none-any.whl.metadata (33 kB)
Collecting fastuuid==0.14.0 (from litellm)
  Downloading fastuuid-0.14.0-cp39-cp39-macosx_11_0_arm64.whl.metadata (1.1 kB)
Collecting httpx==0.28.1 (from litellm)
  Downloading httpx-0.28.1-py3-none-any.whl.metadata (7.1 kB)
Collecting openai==2.24.0 (from litellm)
  Downloading openai-2.24.0-py3-none-any.whl.metadata (29 kB)
Collecting python-dotenv==1.0.1 (from litellm)
  Downloading python_dotenv-1.0.1-py3-none-any.whl.metadata (23 kB)
Collecting tiktoken==0.12.0 (from litellm)
  Downloading tiktoken-0.12.0-cp39-cp39-macosx_11_0_arm64.whl.metadata (6.7 kB)
Collecting importlib-metadata==8.5.0 (from litellm)
  Downloading importlib_metadata-8.5.0-py3-none-any.whl.metadata (4.8 kB)
Collecting tokenizers==0.22.2 (from litellm)
  Downloading tokenizers-0.22.2-cp39-abi3-macosx_11_0_arm64.whl.metadata (7.3 kB)
Collecting click==8.1.8 (from litellm)
  Downloading click-8.1.8-py3-none-any.whl.metadata (2.3 kB)
Collecting jinja2==3.1.6 (from litellm)
  Downloading jinja2-3.1.6-py3-none-any.whl.metadata (2.9 kB)
Collecting aiohttp==3.13.3 (from litellm)
  Downloading aiohttp-3.13.3-cp39-cp39-macosx_11_0_arm64.whl.metadata (8.1 kB)
Collecting pydantic==2.12.5 (from litellm)
  Downloading pydantic-2.12.5-py3-none-any.whl.metadata (90 kB)
Collecting jsonschema==4.23.0 (from litellm)
  Downloading jsonschema-4.23.0-py3-none-any.whl.metadata (7.9 kB)
Collecting aiohappyeyeballs>=2.5.0 (from aiohttp==3.13.3->litellm)
  Downloading aiohappyeyeballs-2.6.1-py3-none-any.whl.metadata (5.9 kB)
Collecting aiosignal>=1.4.0 (from aiohttp==3.13.3->litellm)
  Downloading aiosignal-1.4.0-py3-none-any.whl.metadata (3.7 kB)

[notice] A new release of pip is available: 24.2 -> 26.0.1
[notice] To update, run: /Library/Developer/CommandLineTools/usr/bin/python3 -m pip install --upgrade pip
ERROR: Exception:
Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_vendor/urllib3/response.py", line 438, in _error_catcher
    yield
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_vendor/urllib3/response.py", line 561, in read
    data = self._fp_read(amt) if not fp_closed else b""
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_vendor/urllib3/response.py", line 527, in _fp_read
    return self._fp.read(amt) if amt is not None else self._fp.read()
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_vendor/cachecontrol/filewrapper.py", line 98, in read
    data: bytes = self.__fp.read(amt)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/http/client.py", line 459, in read
    n = self.readinto(b)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/http/client.py", line 503, in readinto
    n = self.fp.readinto(b)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/socket.py", line 704, in readinto
    return self._sock.recv_into(b)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/ssl.py", line 1241, in recv_into
    return self.read(nbytes, buffer)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/ssl.py", line 1099, in read
    return self._sslobj.read(len, buffer)
socket.timeout: The read operation timed out

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/cli/base_command.py", line 105, in _run_wrapper
    status = _inner_run()
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/cli/base_command.py", line 96, in _inner_run
    return self.run(options, args)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/cli/req_command.py", line 67, in wrapper
    return func(self, options, args)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/commands/install.py", line 379, in run
    requirement_set = resolver.resolve(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/resolution/resolvelib/resolver.py", line 95, in resolve
    result = self._result = resolver.resolve(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_vendor/resolvelib/resolvers.py", line 546, in resolve
    state = resolution.resolve(requirements, max_rounds=max_rounds)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_vendor/resolvelib/resolvers.py", line 427, in resolve
    failure_causes = self._attempt_to_pin_criterion(name)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_vendor/resolvelib/resolvers.py", line 239, in _attempt_to_pin_criterion
    criteria = self._get_updated_criteria(candidate)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_vendor/resolvelib/resolvers.py", line 230, in _get_updated_criteria
    self._add_to_criteria(criteria, requirement, parent=candidate)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_vendor/resolvelib/resolvers.py", line 173, in _add_to_criteria
    if not criterion.candidates:
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_vendor/resolvelib/structs.py", line 156, in __bool__
    return bool(self._sequence)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/resolution/resolvelib/found_candidates.py", line 174, in __bool__
    return any(self)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/resolution/resolvelib/found_candidates.py", line 162, in <genexpr>
    return (c for c in iterator if id(c) not in self._incompatible_ids)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/resolution/resolvelib/found_candidates.py", line 53, in _iter_built
    candidate = func()
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/resolution/resolvelib/factory.py", line 186, in _make_candidate_from_link
    base: Optional[BaseCandidate] = self._make_base_candidate_from_link(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/resolution/resolvelib/factory.py", line 232, in _make_base_candidate_from_link
    self._link_candidate_cache[link] = LinkCandidate(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/resolution/resolvelib/candidates.py", line 303, in __init__
    super().__init__(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/resolution/resolvelib/candidates.py", line 158, in __init__
    self.dist = self._prepare()
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/resolution/resolvelib/candidates.py", line 235, in _prepare
    dist = self._prepare_distribution()
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/resolution/resolvelib/candidates.py", line 314, in _prepare_distribution
    return preparer.prepare_linked_requirement(self._ireq, parallel_builds=True)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/operations/prepare.py", line 521, in prepare_linked_requirement
    metadata_dist = self._fetch_metadata_only(req)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/operations/prepare.py", line 373, in _fetch_metadata_only
    return self._fetch_metadata_using_link_data_attr(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/operations/prepare.py", line 393, in _fetch_metadata_using_link_data_attr
    metadata_file = get_http_url(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/operations/prepare.py", line 111, in get_http_url
    from_path, content_type = download(link, temp_dir.path)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/network/download.py", line 148, in __call__
    for chunk in chunks:
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_internal/network/utils.py", line 65, in response_chunks
    for chunk in response.raw.stream(
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_vendor/urllib3/response.py", line 622, in stream
    data = self.read(amt=amt, decode_content=decode_content)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_vendor/urllib3/response.py", line 587, in read
    raise IncompleteRead(self._fp_bytes_read, self.length_remaining)
  File "/Library/Developer/CommandLineTools/Library/Frameworks/Python3.framework/Versions/3.9/lib/python3.9/contextlib.py", line 135, in __exit__
    self.gen.throw(type, value, traceback)
  File "/Users/zhengzixuan/Library/Python/3.9/lib/python/site-packages/pip/_vendor/urllib3/response.py", line 443, in _error_catcher
    raise ReadTimeoutError(self._pool, None, "Read timed out.")
pip._vendor.urllib3.exceptions.ReadTimeoutError: HTTPSConnectionPool(host='files.pythonhosted.org', port=443): Read timed out.
zhengzixuan@MCdeMBP fenbi-helper-master % 

