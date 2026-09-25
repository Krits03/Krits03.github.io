import { FastResponse as e, FastURL as t } from "srvx";
const n = (() => {
	let e = function() {};
	return e.prototype = Object.create(null), Object.freeze(e.prototype), e;
})();
function r(e) {
	return decodeURI(e.includes(`%25`) ? e.replace(/%25/g, `%2525`) : e);
}
const i = `h3.internal.event.`, a = Symbol.for(`${i}res`), o = Symbol.for(`${i}res.headers`), s = Symbol.for(`${i}res.err.headers`), c = Symbol.for(`${i}malformed`);
var l = class {
	app;
	req;
	url;
	context;
	static __is_event__ = !0;
	constructor(e, i, a) {
		this.context = e.context = i || e.context || new n(), this.req = e, this.app = a;
		let o = e._url, s = o && o instanceof URL ? o : new t(e.url);
		if (s.pathname.includes(`%`)) try {
			let e = r(s.pathname);
			e !== s.pathname && (s = new t(`${s.protocol}//${s.host}${e}${s.search}`));
		} catch {
			this[c] = !0;
		}
		this.url = s;
	}
	get res() {
		return this[a] ||= new u();
	}
	get runtime() {
		return this.req.runtime;
	}
	waitUntil(e) {
		this.req.waitUntil?.(e);
	}
	toString() {
		return `[${this.req.method}] ${this.req.url}`;
	}
	toJSON() {
		return this.toString();
	}
	get node() {
		return this.req.runtime?.node;
	}
	get headers() {
		return this.req.headers;
	}
	get path() {
		return this.url.pathname + this.url.search;
	}
	get method() {
		return this.req.method;
	}
}, u = class {
	status;
	statusText;
	get headers() {
		return this[o] ||= new Headers();
	}
	get errHeaders() {
		return this[s] ||= new Headers();
	}
};
const d = /[^\u0009\u0020-\u007E]/g;
function f(e = ``) {
	return e.replace(d, ``);
}
function p(e, t = 200) {
	return !e || (typeof e == `string` && (e = +e), !Number.isInteger(e) || e < 100 || e > 599) ? t : e;
}
var m = class e extends Error {
	get name() {
		return `HTTPError`;
	}
	status;
	statusText;
	headers;
	cause;
	data;
	body;
	unhandled;
	static isError(e) {
		return e instanceof Error && e?.name === `HTTPError`;
	}
	static status(t, n, r) {
		return new e({
			...r,
			statusText: n,
			status: t
		});
	}
	constructor(e, t) {
		let n, r;
		typeof e == `string` ? (n = e, r = t) : r = e;
		let i = p(r?.status || r?.statusCode || r?.cause?.status || r?.cause?.statusCode, 500), a = f(r?.statusText || r?.statusMessage || r?.cause?.statusText || r?.cause?.statusMessage), o = n || r?.message || r?.cause?.message || r?.statusText || r?.statusMessage || [
			`HTTPError`,
			i,
			a
		].filter(Boolean).join(` `);
		super(o, { cause: r }), this.cause = r, this.status = i, this.statusText = a || void 0;
		let s = r?.headers || r?.cause?.headers;
		this.headers = s ? new Headers(s) : void 0, this.unhandled = r?.unhandled ?? r?.cause?.unhandled ?? void 0, this.data = r?.data, this.body = r?.body;
	}
	get statusCode() {
		return this.status;
	}
	get statusMessage() {
		return this.statusText;
	}
	toJSON() {
		let e = this.unhandled;
		return {
			status: this.status,
			statusText: this.statusText,
			unhandled: e,
			message: e ? `HTTPError` : this.message,
			data: e ? void 0 : this.data,
			...e ? void 0 : this.body
		};
	}
};
function h(e, t) {
	if (e == null) return !0;
	if (t !== `object`) return t === `boolean` || t === `number` || t === `string`;
	if (typeof e.toJSON == `function` || Array.isArray(e)) return !0;
	if (typeof e.pipe == `function` || typeof e.pipeTo == `function`) return !1;
	if (e instanceof n) return !0;
	let r = Object.getPrototypeOf(e);
	return r === Object.prototype || r === null;
}
const g = Symbol.for(`h3.internal.event.dispose`), _ = Symbol.for(`h3.notFound`), v = Symbol.for(`h3.handled`);
function y(e, t, n = {}) {
	if (typeof e?.then == `function`) return e.then((e) => y(e, t, n), (e) => y(b(e), t, n));
	let r;
	try {
		r = S(e, t, n);
	} catch (e) {
		return y(b(e), t, n);
	}
	if (typeof r?.then == `function`) return y(r, t, n);
	let { onResponse: i } = n;
	return i ? Promise.resolve().then(() => i(r, t)).catch((e) => {
		n.silent || console.error(e);
	}).then(() => t[g]?.observe(r, e) ?? r) : t[g]?.observe(r, e) ?? r;
}
function b(e) {
	if (e === _ || e === v || e instanceof Error) return e;
	if (typeof e == `number`) return new m({ status: e });
	let t = new m({
		status: 500,
		unhandled: !0
	});
	return t.cause = e, t;
}
var x = class {
	#headers;
	#init;
	body;
	constructor(e, t) {
		this.body = e, this.#init = t;
	}
	get status() {
		return this.#init?.status;
	}
	get statusText() {
		return this.#init?.statusText;
	}
	get headers() {
		return this.#headers ||= new Headers(this.#init?.headers);
	}
};
function S(t, n, r, i) {
	if (t === v) return new e(null);
	if (t === _ && (t = new m({
		status: 404,
		message: `Cannot find any route matching [${n.req.method}] ${n.url}`
	})), t && t instanceof Error) {
		let e = m.isError(t), o = e ? t : new m(t);
		e || (o.unhandled = !0, t?.stack && (o.stack = t.stack)), o.unhandled && !r.silent && console.error(o);
		let { onError: c } = r, l = n[a]?.[s];
		return c && !i ? Promise.resolve().then(() => c(o, n)).catch((e) => e).then((e) => S(e ?? t, n, r, !0)) : A(o, r.debug, l);
	}
	let c = n[a], l = c?.[o];
	if (n[a] = void 0, !(t instanceof Response)) {
		let i = O(t, n, r), a = i.status || c?.status;
		return new e(k(n.req.method, a) ? null : i.body, {
			status: a,
			statusText: i.statusText || c?.statusText,
			headers: i.headers && l ? C(i.headers, l) : i.headers || l
		});
	}
	if (t.status >= 400 && (l = c?.[s]), l && !i) try {
		C(t.headers, l, t.headers);
	} catch {
		return new e(k(n.req.method, t.status) ? null : t.body, {
			status: t.status,
			statusText: t.statusText,
			headers: C(t.headers, l)
		});
	}
	return n.req.method === `HEAD` && t.body !== null ? new e(null, {
		status: t.status,
		statusText: t.statusText,
		headers: t.headers
	}) : t;
}
function C(e, t, n = new Headers(e)) {
	for (let [e, r] of t) e === `set-cookie` ? n.append(e, r) : n.set(e, r);
	return n;
}
const w = (e) => (...t) => {
	throw Error(`Headers are frozen (${e} ${t.join(`, `)})`);
};
var T = class extends Headers {
	set = w(`set`);
	append = w(`append`);
	delete = w(`delete`);
};
const E = new T({ "content-length": `0` }), D = new T({ "content-type": `application/json;charset=UTF-8` });
function O(e, t, n) {
	if (e == null) return {
		body: ``,
		headers: E
	};
	let r = typeof e;
	if (r === `string`) return { body: e };
	if (e instanceof Uint8Array) return {
		body: e,
		headers: new Headers({ "content-length": e.byteLength.toString() })
	};
	if (e instanceof x || e?.constructor?.name === `HTTPResponse`) return e;
	if (h(e, r)) return {
		body: JSON.stringify(e, void 0, n.debug ? 2 : void 0),
		headers: D
	};
	if (r === `bigint`) return {
		body: e.toString(),
		headers: D
	};
	if (e instanceof Blob) {
		let t = new Headers({
			"content-type": e.type,
			"content-length": e.size.toString()
		}), n = e.name;
		return n && (n = encodeURIComponent(n), t.set(`content-disposition`, `filename="${n}"; filename*=UTF-8''${n}`)), {
			body: e.stream(),
			headers: t
		};
	}
	return r === `symbol` ? { body: e.toString() } : r === `function` ? { body: `${e.name}()` } : { body: e };
}
function k(e, t) {
	return e === `HEAD` || t === 100 || t === 101 || t === 102 || t === 204 || t === 205 || t === 304;
}
function A(t, n, r) {
	let i = t.headers ? C(D, t.headers) : new Headers(D);
	return r && (i = C(i, r)), new e(JSON.stringify({
		...t.toJSON(),
		stack: n && t.stack ? t.stack.split(`
`).map((e) => e.trim()) : void 0
	}, void 0, n ? 2 : void 0), {
		status: t.status,
		statusText: t.statusText,
		headers: i
	});
}
function j(e) {
	let t = (e, t) => t(e);
	for (let n = e.length - 1; n >= 0; n--) {
		let r = e[n], i = t;
		t = (e, t) => N(r, e, t, i);
	}
	return t;
}
function M(e, t) {
	let n = j(e);
	return function(e) {
		return n(e, t);
	};
}
function N(e, t, n, r) {
	let i, a, o = () => i ? a : (i = !0, a = r(t, n), a), s = e(t, o);
	return P(s) ? o() : typeof s?.then == `function` ? s.then((e) => P(e) ? o() : e) : s;
}
function P(e) {
	return e === void 0 || e === _;
}
function F(e) {
	if (typeof e == `function`) return I(e);
	let t = e.handler || (e.fetch ? function(t) {
		return e.fetch(t.req);
	} : L);
	return Object.assign(I(e.middleware?.length ? M(e.middleware, t) : t), e);
}
function I(e) {
	return `fetch` in e ? e : Object.assign(e, { fetch: (t) => {
		typeof t == `string` && (t = new URL(t, `http://_`)), t instanceof URL && (t = new Request(t));
		let n = new l(t);
		try {
			return Promise.resolve(y(e(n), n));
		} catch (e) {
			return Promise.resolve(y(b(e), n));
		}
	} });
}
const L = () => _;
String.raw`(?:^|/)(?:\.|%(?:25)*2e){1,2}(?:/|$)`, String.raw`%(?:25)*(?:2f|5c)`;
const R = F;
export { m as HTTPError, R as defineEventHandler };
