(self.webpackChunk_N_E = self.webpackChunk_N_E || []).push([[888], {
    51131: function(e, t, n) {
        "use strict";
        n.d(t, {
            J: function() {
                return r
            }
        });
        let r = "production"
    },
    64487: function(e, t, n) {
        "use strict";
        n.d(t, {
            $e: function() {
                return s
            },
            Tb: function() {
                return i
            },
            e: function() {
                return o
            }
        });
        var r = n(95659);
        function i(e, t) {
            return (0,
            r.Gd)().captureException(e, {
                captureContext: t
            })
        }
        function o(e) {
            (0,
            r.Gd)().configureScope(e)
        }
        function s(e) {
            (0,
            r.Gd)().withScope(e)
        }
    },
    95659: function(e, t, n) {
        "use strict";
        n.d(t, {
            Gd: function() {
                return h
            },
            cu: function() {
                return d
            }
        });
        var r = n(62844)
          , i = n(21170)
          , o = n(12343)
          , s = n(71235)
          , a = n(51131)
          , l = n(10350)
          , u = n(9015);
        class c {
            constructor(e, t=new l.s, n=4) {
                this._version = n,
                this._stack = [{
                    scope: t
                }],
                e && this.bindClient(e)
            }
            isOlderThan(e) {
                return this._version < e
            }
            bindClient(e) {
                let t = this.getStackTop();
                t.client = e,
                e && e.setupIntegrations && e.setupIntegrations()
            }
            pushScope() {
                let e = l.s.clone(this.getScope());
                return this.getStack().push({
                    client: this.getClient(),
                    scope: e
                }),
                e
            }
            popScope() {
                return !(this.getStack().length <= 1) && !!this.getStack().pop()
            }
            withScope(e) {
                let t = this.pushScope();
                try {
                    e(t)
                } finally {
                    this.popScope()
                }
            }
            getClient() {
                return this.getStackTop().client
            }
            getScope() {
                return this.getStackTop().scope
            }
            getStack() {
                return this._stack
            }
            getStackTop() {
                return this._stack[this._stack.length - 1]
            }
            captureException(e, t) {
                let n = this._lastEventId = t && t.event_id ? t.event_id : (0,
                r.DM)()
                  , i = Error("Sentry syntheticException");
                return this._withClient((r,o)=>{
                    r.captureException(e, {
                        originalException: e,
                        syntheticException: i,
                        ...t,
                        event_id: n
                    }, o)
                }
                ),
                n
            }
            captureMessage(e, t, n) {
                let i = this._lastEventId = n && n.event_id ? n.event_id : (0,
                r.DM)()
                  , o = Error(e);
                return this._withClient((r,s)=>{
                    r.captureMessage(e, t, {
                        originalException: e,
                        syntheticException: o,
                        ...n,
                        event_id: i
                    }, s)
                }
                ),
                i
            }
            captureEvent(e, t) {
                let n = t && t.event_id ? t.event_id : (0,
                r.DM)();
                return e.type || (this._lastEventId = n),
                this._withClient((r,i)=>{
                    r.captureEvent(e, {
                        ...t,
                        event_id: n
                    }, i)
                }
                ),
                n
            }
            lastEventId() {
                return this._lastEventId
            }
            addBreadcrumb(e, t) {
                let {scope: n, client: r} = this.getStackTop();
                if (!r)
                    return;
                let {beforeBreadcrumb: s=null, maxBreadcrumbs: a=100} = r.getOptions && r.getOptions() || {};
                if (a <= 0)
                    return;
                let l = (0,
                i.yW)()
                  , u = {
                    timestamp: l,
                    ...e
                }
                  , c = s ? (0,
                o.Cf)(()=>s(u, t)) : u;
                null !== c && (r.emit && r.emit("beforeAddBreadcrumb", c, t),
                n.addBreadcrumb(c, a))
            }
            setUser(e) {
                this.getScope().setUser(e)
            }
            setTags(e) {
                this.getScope().setTags(e)
            }
            setExtras(e) {
                this.getScope().setExtras(e)
            }
            setTag(e, t) {
                this.getScope().setTag(e, t)
            }
            setExtra(e, t) {
                this.getScope().setExtra(e, t)
            }
            setContext(e, t) {
                this.getScope().setContext(e, t)
            }
            configureScope(e) {
                let {scope: t, client: n} = this.getStackTop();
                n && e(t)
            }
            run(e) {
                let t = p(this);
                try {
                    e(this)
                } finally {
                    p(t)
                }
            }
            getIntegration(e) {
                let t = this.getClient();
                if (!t)
                    return null;
                try {
                    return t.getIntegration(e)
                } catch (n) {
                    return ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && o.kg.warn(`Cannot retrieve integration ${e.id} from the current Hub`),
                    null
                }
            }
            startTransaction(e, t) {
                let n = this._callExtensionMethod("startTransaction", e, t);
                return ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && !n && console.warn(`Tracing extension 'startTransaction' has not been added. Call 'addTracingExtensions' before calling 'init':
Sentry.addTracingExtensions();
Sentry.init({...});
`),
                n
            }
            traceHeaders() {
                return this._callExtensionMethod("traceHeaders")
            }
            captureSession(e=!1) {
                if (e)
                    return this.endSession();
                this._sendSessionUpdate()
            }
            endSession() {
                let e = this.getStackTop()
                  , t = e.scope
                  , n = t.getSession();
                n && (0,
                u.RJ)(n),
                this._sendSessionUpdate(),
                t.setSession()
            }
            startSession(e) {
                let {scope: t, client: n} = this.getStackTop()
                  , {release: r, environment: i=a.J} = n && n.getOptions() || {}
                  , {userAgent: o} = s.n2.navigator || {}
                  , l = (0,
                u.Hv)({
                    release: r,
                    environment: i,
                    user: t.getUser(),
                    ...o && {
                        userAgent: o
                    },
                    ...e
                })
                  , c = t.getSession && t.getSession();
                return c && "ok" === c.status && (0,
                u.CT)(c, {
                    status: "exited"
                }),
                this.endSession(),
                t.setSession(l),
                l
            }
            shouldSendDefaultPii() {
                let e = this.getClient()
                  , t = e && e.getOptions();
                return Boolean(t && t.sendDefaultPii)
            }
            _sendSessionUpdate() {
                let {scope: e, client: t} = this.getStackTop()
                  , n = e.getSession();
                n && t && t.captureSession && t.captureSession(n)
            }
            _withClient(e) {
                let {scope: t, client: n} = this.getStackTop();
                n && e(n, t)
            }
            _callExtensionMethod(e, ...t) {
                let n = d()
                  , r = n.__SENTRY__;
                if (r && r.extensions && "function" == typeof r.extensions[e])
                    return r.extensions[e].apply(this, t);
                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && o.kg.warn(`Extension method ${e} couldn't be found, doing nothing.`)
            }
        }
        function d() {
            return s.n2.__SENTRY__ = s.n2.__SENTRY__ || {
                extensions: {},
                hub: void 0
            },
            s.n2
        }
        function p(e) {
            let t = d()
              , n = f(t);
            return g(t, e),
            n
        }
        function h() {
            let e = d();
            if (e.__SENTRY__ && e.__SENTRY__.acs) {
                let t = e.__SENTRY__.acs.getCurrentHub();
                if (t)
                    return t
            }
            return function(e=d()) {
                return (!(e && e.__SENTRY__ && e.__SENTRY__.hub) || f(e).isOlderThan(4)) && g(e, new c),
                f(e)
            }(e)
        }
        function f(e) {
            return (0,
            s.YO)("hub", ()=>new c, e)
        }
        function g(e, t) {
            if (!e)
                return !1;
            let n = e.__SENTRY__ = e.__SENTRY__ || {};
            return n.hub = t,
            !0
        }
    },
    10350: function(e, t, n) {
        "use strict";
        n.d(t, {
            c: function() {
                return p
            },
            s: function() {
                return c
            }
        });
        var r = n(67597)
          , i = n(21170)
          , o = n(96893)
          , s = n(12343)
          , a = n(62844)
          , l = n(71235)
          , u = n(9015);
        class c {
            constructor() {
                this._notifyingListeners = !1,
                this._scopeListeners = [],
                this._eventProcessors = [],
                this._breadcrumbs = [],
                this._attachments = [],
                this._user = {},
                this._tags = {},
                this._extra = {},
                this._contexts = {},
                this._sdkProcessingMetadata = {},
                this._propagationContext = h()
            }
            static clone(e) {
                let t = new c;
                return e && (t._breadcrumbs = [...e._breadcrumbs],
                t._tags = {
                    ...e._tags
                },
                t._extra = {
                    ...e._extra
                },
                t._contexts = {
                    ...e._contexts
                },
                t._user = e._user,
                t._level = e._level,
                t._span = e._span,
                t._session = e._session,
                t._transactionName = e._transactionName,
                t._fingerprint = e._fingerprint,
                t._eventProcessors = [...e._eventProcessors],
                t._requestSession = e._requestSession,
                t._attachments = [...e._attachments],
                t._sdkProcessingMetadata = {
                    ...e._sdkProcessingMetadata
                },
                t._propagationContext = {
                    ...e._propagationContext
                }),
                t
            }
            addScopeListener(e) {
                this._scopeListeners.push(e)
            }
            addEventProcessor(e) {
                return this._eventProcessors.push(e),
                this
            }
            setUser(e) {
                return this._user = e || {},
                this._session && (0,
                u.CT)(this._session, {
                    user: e
                }),
                this._notifyScopeListeners(),
                this
            }
            getUser() {
                return this._user
            }
            getRequestSession() {
                return this._requestSession
            }
            setRequestSession(e) {
                return this._requestSession = e,
                this
            }
            setTags(e) {
                return this._tags = {
                    ...this._tags,
                    ...e
                },
                this._notifyScopeListeners(),
                this
            }
            setTag(e, t) {
                return this._tags = {
                    ...this._tags,
                    [e]: t
                },
                this._notifyScopeListeners(),
                this
            }
            setExtras(e) {
                return this._extra = {
                    ...this._extra,
                    ...e
                },
                this._notifyScopeListeners(),
                this
            }
            setExtra(e, t) {
                return this._extra = {
                    ...this._extra,
                    [e]: t
                },
                this._notifyScopeListeners(),
                this
            }
            setFingerprint(e) {
                return this._fingerprint = e,
                this._notifyScopeListeners(),
                this
            }
            setLevel(e) {
                return this._level = e,
                this._notifyScopeListeners(),
                this
            }
            setTransactionName(e) {
                return this._transactionName = e,
                this._notifyScopeListeners(),
                this
            }
            setContext(e, t) {
                return null === t ? delete this._contexts[e] : this._contexts[e] = t,
                this._notifyScopeListeners(),
                this
            }
            setSpan(e) {
                return this._span = e,
                this._notifyScopeListeners(),
                this
            }
            getSpan() {
                return this._span
            }
            getTransaction() {
                let e = this.getSpan();
                return e && e.transaction
            }
            setSession(e) {
                return e ? this._session = e : delete this._session,
                this._notifyScopeListeners(),
                this
            }
            getSession() {
                return this._session
            }
            update(e) {
                if (!e)
                    return this;
                if ("function" == typeof e) {
                    let t = e(this);
                    return t instanceof c ? t : this
                }
                return e instanceof c ? (this._tags = {
                    ...this._tags,
                    ...e._tags
                },
                this._extra = {
                    ...this._extra,
                    ...e._extra
                },
                this._contexts = {
                    ...this._contexts,
                    ...e._contexts
                },
                e._user && Object.keys(e._user).length && (this._user = e._user),
                e._level && (this._level = e._level),
                e._fingerprint && (this._fingerprint = e._fingerprint),
                e._requestSession && (this._requestSession = e._requestSession),
                e._propagationContext && (this._propagationContext = e._propagationContext)) : (0,
                r.PO)(e) && (this._tags = {
                    ...this._tags,
                    ...e.tags
                },
                this._extra = {
                    ...this._extra,
                    ...e.extra
                },
                this._contexts = {
                    ...this._contexts,
                    ...e.contexts
                },
                e.user && (this._user = e.user),
                e.level && (this._level = e.level),
                e.fingerprint && (this._fingerprint = e.fingerprint),
                e.requestSession && (this._requestSession = e.requestSession),
                e.propagationContext && (this._propagationContext = e.propagationContext)),
                this
            }
            clear() {
                return this._breadcrumbs = [],
                this._tags = {},
                this._extra = {},
                this._user = {},
                this._contexts = {},
                this._level = void 0,
                this._transactionName = void 0,
                this._fingerprint = void 0,
                this._requestSession = void 0,
                this._span = void 0,
                this._session = void 0,
                this._notifyScopeListeners(),
                this._attachments = [],
                this._propagationContext = h(),
                this
            }
            addBreadcrumb(e, t) {
                let n = "number" == typeof t ? t : 100;
                if (n <= 0)
                    return this;
                let r = {
                    timestamp: (0,
                    i.yW)(),
                    ...e
                };
                return this._breadcrumbs = [...this._breadcrumbs, r].slice(-n),
                this._notifyScopeListeners(),
                this
            }
            getLastBreadcrumb() {
                return this._breadcrumbs[this._breadcrumbs.length - 1]
            }
            clearBreadcrumbs() {
                return this._breadcrumbs = [],
                this._notifyScopeListeners(),
                this
            }
            addAttachment(e) {
                return this._attachments.push(e),
                this
            }
            getAttachments() {
                return this._attachments
            }
            clearAttachments() {
                return this._attachments = [],
                this
            }
            applyToEvent(e, t={}) {
                if (this._extra && Object.keys(this._extra).length && (e.extra = {
                    ...this._extra,
                    ...e.extra
                }),
                this._tags && Object.keys(this._tags).length && (e.tags = {
                    ...this._tags,
                    ...e.tags
                }),
                this._user && Object.keys(this._user).length && (e.user = {
                    ...this._user,
                    ...e.user
                }),
                this._contexts && Object.keys(this._contexts).length && (e.contexts = {
                    ...this._contexts,
                    ...e.contexts
                }),
                this._level && (e.level = this._level),
                this._transactionName && (e.transaction = this._transactionName),
                this._span) {
                    e.contexts = {
                        trace: this._span.getTraceContext(),
                        ...e.contexts
                    };
                    let n = this._span.transaction;
                    if (n) {
                        e.sdkProcessingMetadata = {
                            dynamicSamplingContext: n.getDynamicSamplingContext(),
                            ...e.sdkProcessingMetadata
                        };
                        let r = n.name;
                        r && (e.tags = {
                            transaction: r,
                            ...e.tags
                        })
                    }
                }
                return this._applyFingerprint(e),
                e.breadcrumbs = [...e.breadcrumbs || [], ...this._breadcrumbs],
                e.breadcrumbs = e.breadcrumbs.length > 0 ? e.breadcrumbs : void 0,
                e.sdkProcessingMetadata = {
                    ...e.sdkProcessingMetadata,
                    ...this._sdkProcessingMetadata,
                    propagationContext: this._propagationContext
                },
                this._notifyEventProcessors([...d(), ...this._eventProcessors], e, t)
            }
            setSDKProcessingMetadata(e) {
                return this._sdkProcessingMetadata = {
                    ...this._sdkProcessingMetadata,
                    ...e
                },
                this
            }
            setPropagationContext(e) {
                return this._propagationContext = e,
                this
            }
            getPropagationContext() {
                return this._propagationContext
            }
            _notifyEventProcessors(e, t, n, i=0) {
                return new o.cW((o,a)=>{
                    let l = e[i];
                    if (null === t || "function" != typeof l)
                        o(t);
                    else {
                        let u = l({
                            ...t
                        }, n);
                        ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && l.id && null === u && s.kg.log(`Event processor "${l.id}" dropped event`),
                        (0,
                        r.J8)(u) ? u.then(t=>this._notifyEventProcessors(e, t, n, i + 1).then(o)).then(null, a) : this._notifyEventProcessors(e, u, n, i + 1).then(o).then(null, a)
                    }
                }
                )
            }
            _notifyScopeListeners() {
                this._notifyingListeners || (this._notifyingListeners = !0,
                this._scopeListeners.forEach(e=>{
                    e(this)
                }
                ),
                this._notifyingListeners = !1)
            }
            _applyFingerprint(e) {
                e.fingerprint = e.fingerprint ? (0,
                a.lE)(e.fingerprint) : [],
                this._fingerprint && (e.fingerprint = e.fingerprint.concat(this._fingerprint)),
                e.fingerprint && !e.fingerprint.length && delete e.fingerprint
            }
        }
        function d() {
            return (0,
            l.YO)("globalEventProcessors", ()=>[])
        }
        function p(e) {
            d().push(e)
        }
        function h() {
            return {
                traceId: (0,
                a.DM)(),
                spanId: (0,
                a.DM)().substring(16),
                sampled: !1
            }
        }
    },
    9015: function(e, t, n) {
        "use strict";
        n.d(t, {
            CT: function() {
                return a
            },
            Hv: function() {
                return s
            },
            RJ: function() {
                return l
            }
        });
        var r = n(21170)
          , i = n(62844)
          , o = n(20535);
        function s(e) {
            let t = (0,
            r.ph)()
              , n = {
                sid: (0,
                i.DM)(),
                init: !0,
                timestamp: t,
                started: t,
                duration: 0,
                status: "ok",
                errors: 0,
                ignoreDuration: !1,
                toJSON: ()=>(0,
                o.Jr)({
                    sid: `${n.sid}`,
                    init: n.init,
                    started: new Date(1e3 * n.started).toISOString(),
                    timestamp: new Date(1e3 * n.timestamp).toISOString(),
                    status: n.status,
                    errors: n.errors,
                    did: "number" == typeof n.did || "string" == typeof n.did ? `${n.did}` : void 0,
                    duration: n.duration,
                    attrs: {
                        release: n.release,
                        environment: n.environment,
                        ip_address: n.ipAddress,
                        user_agent: n.userAgent
                    }
                })
            };
            return e && a(n, e),
            n
        }
        function a(e, t={}) {
            if (!t.user || (!e.ipAddress && t.user.ip_address && (e.ipAddress = t.user.ip_address),
            e.did || t.did || (e.did = t.user.id || t.user.email || t.user.username)),
            e.timestamp = t.timestamp || (0,
            r.ph)(),
            t.ignoreDuration && (e.ignoreDuration = t.ignoreDuration),
            t.sid && (e.sid = 32 === t.sid.length ? t.sid : (0,
            i.DM)()),
            void 0 !== t.init && (e.init = t.init),
            !e.did && t.did && (e.did = `${t.did}`),
            "number" == typeof t.started && (e.started = t.started),
            e.ignoreDuration)
                e.duration = void 0;
            else if ("number" == typeof t.duration)
                e.duration = t.duration;
            else {
                let n = e.timestamp - e.started;
                e.duration = n >= 0 ? n : 0
            }
            t.release && (e.release = t.release),
            t.environment && (e.environment = t.environment),
            !e.ipAddress && t.ipAddress && (e.ipAddress = t.ipAddress),
            !e.userAgent && t.userAgent && (e.userAgent = t.userAgent),
            "number" == typeof t.errors && (e.errors = t.errors),
            t.status && (e.status = t.status)
        }
        function l(e, t) {
            let n = {};
            t ? n = {
                status: t
            } : "ok" === e.status && (n = {
                status: "exited"
            }),
            a(e, n)
        }
    },
    58464: function(e, t, n) {
        "use strict";
        n.d(t, {
            Rt: function() {
                return s
            },
            l4: function() {
                return a
            },
            qT: function() {
                return l
            }
        });
        var r = n(67597)
          , i = n(71235);
        let o = (0,
        i.Rf)();
        function s(e, t={}) {
            try {
                let n, i = e, o = [], s = 0, a = 0, l = Array.isArray(t) ? t : t.keyAttrs, u = !Array.isArray(t) && t.maxStringLength || 80;
                for (; i && s++ < 5 && (n = function(e, t) {
                    let n, i, o, s, a;
                    let l = [];
                    if (!e || !e.tagName)
                        return "";
                    l.push(e.tagName.toLowerCase());
                    let u = t && t.length ? t.filter(t=>e.getAttribute(t)).map(t=>[t, e.getAttribute(t)]) : null;
                    if (u && u.length)
                        u.forEach(e=>{
                            l.push(`[${e[0]}="${e[1]}"]`)
                        }
                        );
                    else if (e.id && l.push(`#${e.id}`),
                    (n = e.className) && (0,
                    r.HD)(n))
                        for (a = 0,
                        i = n.split(/\s+/); a < i.length; a++)
                            l.push(`.${i[a]}`);
                    let c = ["aria-label", "type", "name", "title", "alt"];
                    for (a = 0; a < c.length; a++)
                        o = c[a],
                        (s = e.getAttribute(o)) && l.push(`[${o}="${s}"]`);
                    return l.join("")
                }(i, l),
                "html" !== n && (!(s > 1) || !(a + 3 * o.length + n.length >= u))); )
                    o.push(n),
                    a += n.length,
                    i = i.parentNode;
                return o.reverse().join(" > ")
            } catch (c) {
                return "<unknown>"
            }
        }
        function a() {
            try {
                return o.document.location.href
            } catch (e) {
                return ""
            }
        }
        function l(e) {
            return o.document && o.document.querySelector ? o.document.querySelector(e) : null
        }
    },
    68518: function(e, t, n) {
        "use strict";
        function r() {
            return "undefined" != typeof __SENTRY_BROWSER_BUNDLE__ && !!__SENTRY_BROWSER_BUNDLE__
        }
        function i() {
            return "npm"
        }
        n.d(t, {
            S: function() {
                return i
            },
            n: function() {
                return r
            }
        })
    },
    67597: function(e, t, n) {
        "use strict";
        n.d(t, {
            Cy: function() {
                return m
            },
            HD: function() {
                return u
            },
            J8: function() {
                return g
            },
            Kj: function() {
                return f
            },
            PO: function() {
                return d
            },
            TX: function() {
                return a
            },
            V9: function() {
                return y
            },
            VW: function() {
                return s
            },
            VZ: function() {
                return i
            },
            cO: function() {
                return p
            },
            fm: function() {
                return l
            },
            i2: function() {
                return _
            },
            kK: function() {
                return h
            },
            pt: function() {
                return c
            }
        });
        let r = Object.prototype.toString;
        function i(e) {
            switch (r.call(e)) {
            case "[object Error]":
            case "[object Exception]":
            case "[object DOMException]":
                return !0;
            default:
                return y(e, Error)
            }
        }
        function o(e, t) {
            return r.call(e) === `[object ${t}]`
        }
        function s(e) {
            return o(e, "ErrorEvent")
        }
        function a(e) {
            return o(e, "DOMError")
        }
        function l(e) {
            return o(e, "DOMException")
        }
        function u(e) {
            return o(e, "String")
        }
        function c(e) {
            return null === e || "object" != typeof e && "function" != typeof e
        }
        function d(e) {
            return o(e, "Object")
        }
        function p(e) {
            return "undefined" != typeof Event && y(e, Event)
        }
        function h(e) {
            return "undefined" != typeof Element && y(e, Element)
        }
        function f(e) {
            return o(e, "RegExp")
        }
        function g(e) {
            return Boolean(e && e.then && "function" == typeof e.then)
        }
        function m(e) {
            return d(e) && "nativeEvent"in e && "preventDefault"in e && "stopPropagation"in e
        }
        function _(e) {
            return "number" == typeof e && e != e
        }
        function y(e, t) {
            try {
                return e instanceof t
            } catch (n) {
                return !1
            }
        }
    },
    12343: function(e, t, n) {
        "use strict";
        let r;
        n.d(t, {
            Cf: function() {
                return s
            },
            RU: function() {
                return o
            },
            kg: function() {
                return r
            }
        });
        var i = n(71235);
        let o = ["debug", "info", "warn", "error", "log", "assert", "trace"];
        function s(e) {
            if (!("console"in i.n2))
                return e();
            let t = i.n2.console
              , n = {};
            o.forEach(e=>{
                let r = t[e] && t[e].__sentry_original__;
                e in t && r && (n[e] = t[e],
                t[e] = r)
            }
            );
            try {
                return e()
            } finally {
                Object.keys(n).forEach(e=>{
                    t[e] = n[e]
                }
                )
            }
        }
        function a() {
            let e = !1
              , t = {
                enable: ()=>{
                    e = !0
                }
                ,
                disable: ()=>{
                    e = !1
                }
            };
            return "undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__ ? o.forEach(n=>{
                t[n] = (...t)=>{
                    e && s(()=>{
                        i.n2.console[n](`Sentry Logger [${n}]:`, ...t)
                    }
                    )
                }
            }
            ) : o.forEach(e=>{
                t[e] = ()=>void 0
            }
            ),
            t
        }
        r = "undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__ ? (0,
        i.YO)("logger", a) : a()
    },
    62844: function(e, t, n) {
        "use strict";
        n.d(t, {
            DM: function() {
                return o
            },
            Db: function() {
                return l
            },
            EG: function() {
                return u
            },
            YO: function() {
                return c
            },
            jH: function() {
                return a
            },
            lE: function() {
                return d
            }
        });
        var r = n(20535)
          , i = n(71235);
        function o() {
            let e = i.n2
              , t = e.crypto || e.msCrypto;
            if (t && t.randomUUID)
                return t.randomUUID().replace(/-/g, "");
            let n = t && t.getRandomValues ? ()=>t.getRandomValues(new Uint8Array(1))[0] : ()=>16 * Math.random();
            return "10000000100040008000100000000000".replace(/[018]/g, e=>(e ^ (15 & n()) >> e / 4).toString(16))
        }
        function s(e) {
            return e.exception && e.exception.values ? e.exception.values[0] : void 0
        }
        function a(e) {
            let {message: t, event_id: n} = e;
            if (t)
                return t;
            let r = s(e);
            return r ? r.type && r.value ? `${r.type}: ${r.value}` : r.type || r.value || n || "<unknown>" : n || "<unknown>"
        }
        function l(e, t, n) {
            let r = e.exception = e.exception || {}
              , i = r.values = r.values || []
              , o = i[0] = i[0] || {};
            o.value || (o.value = t || ""),
            o.type || (o.type = n || "Error")
        }
        function u(e, t) {
            let n = s(e);
            if (!n)
                return;
            let r = n.mechanism;
            if (n.mechanism = {
                type: "generic",
                handled: !0,
                ...r,
                ...t
            },
            t && "data"in t) {
                let i = {
                    ...r && r.data,
                    ...t.data
                };
                n.mechanism.data = i
            }
        }
        function c(e) {
            if (e && e.__sentry_captured__)
                return !0;
            try {
                (0,
                r.xp)(e, "__sentry_captured__", !0)
            } catch (t) {}
            return !1
        }
        function d(e) {
            return Array.isArray(e) ? e : [e]
        }
    },
    61422: function(e, t, n) {
        "use strict";
        n.d(t, {
            KV: function() {
                return o
            },
            l$: function() {
                return s
            }
        });
        var r = n(68518);
        e = n.hmd(e);
        var i = n(34155);
        function o() {
            return !(0,
            r.n)() && "[object process]" === Object.prototype.toString.call(void 0 !== i ? i : 0)
        }
        function s(e, t) {
            return e.require(t)
        }
    },
    20535: function(e, t, n) {
        "use strict";
        n.d(t, {
            $Q: function() {
                return l
            },
            HK: function() {
                return u
            },
            Jr: function() {
                return g
            },
            Sh: function() {
                return d
            },
            _j: function() {
                return c
            },
            hl: function() {
                return s
            },
            xp: function() {
                return a
            },
            zf: function() {
                return f
            }
        });
        var r = n(58464)
          , i = n(67597)
          , o = n(57321);
        function s(e, t, n) {
            if (!(t in e))
                return;
            let r = e[t]
              , i = n(r);
            if ("function" == typeof i)
                try {
                    l(i, r)
                } catch (o) {}
            e[t] = i
        }
        function a(e, t, n) {
            Object.defineProperty(e, t, {
                value: n,
                writable: !0,
                configurable: !0
            })
        }
        function l(e, t) {
            let n = t.prototype || {};
            e.prototype = t.prototype = n,
            a(e, "__sentry_original__", t)
        }
        function u(e) {
            return e.__sentry_original__
        }
        function c(e) {
            return Object.keys(e).map(t=>`${encodeURIComponent(t)}=${encodeURIComponent(e[t])}`).join("&")
        }
        function d(e) {
            if ((0,
            i.VZ)(e))
                return {
                    message: e.message,
                    name: e.name,
                    stack: e.stack,
                    ...h(e)
                };
            if (!(0,
            i.cO)(e))
                return e;
            {
                let t = {
                    type: e.type,
                    target: p(e.target),
                    currentTarget: p(e.currentTarget),
                    ...h(e)
                };
                return "undefined" != typeof CustomEvent && (0,
                i.V9)(e, CustomEvent) && (t.detail = e.detail),
                t
            }
        }
        function p(e) {
            try {
                return (0,
                i.kK)(e) ? (0,
                r.Rt)(e) : Object.prototype.toString.call(e)
            } catch (t) {
                return "<unknown>"
            }
        }
        function h(e) {
            if ("object" != typeof e || null === e)
                return {};
            {
                let t = {};
                for (let n in e)
                    Object.prototype.hasOwnProperty.call(e, n) && (t[n] = e[n]);
                return t
            }
        }
        function f(e, t=40) {
            let n = Object.keys(d(e));
            if (n.sort(),
            !n.length)
                return "[object has no keys]";
            if (n[0].length >= t)
                return (0,
                o.$G)(n[0], t);
            for (let r = n.length; r > 0; r--) {
                let i = n.slice(0, r).join(", ");
                if (!(i.length > t)) {
                    if (r === n.length)
                        return i;
                    return (0,
                    o.$G)(i, t)
                }
            }
            return ""
        }
        function g(e) {
            let t = new Map;
            return function e(t, n) {
                if ((0,
                i.PO)(t)) {
                    let r = n.get(t);
                    if (void 0 !== r)
                        return r;
                    let o = {};
                    for (let s of (n.set(t, o),
                    Object.keys(t)))
                        void 0 !== t[s] && (o[s] = e(t[s], n));
                    return o
                }
                if (Array.isArray(t)) {
                    let a = n.get(t);
                    if (void 0 !== a)
                        return a;
                    let l = [];
                    return n.set(t, l),
                    t.forEach(t=>{
                        l.push(e(t, n))
                    }
                    ),
                    l
                }
                return t
            }(e, t)
        }
    },
    57321: function(e, t, n) {
        "use strict";
        n.d(t, {
            $G: function() {
                return i
            },
            U0: function() {
                return s
            },
            nK: function() {
                return o
            }
        });
        var r = n(67597);
        function i(e, t=0) {
            return "string" != typeof e || 0 === t ? e : e.length <= t ? e : `${e.slice(0, t)}...`
        }
        function o(e, t) {
            if (!Array.isArray(e))
                return "";
            let n = [];
            for (let r = 0; r < e.length; r++) {
                let i = e[r];
                try {
                    n.push(String(i))
                } catch (o) {
                    n.push("[value cannot be serialized]")
                }
            }
            return n.join(t)
        }
        function s(e, t=[], n=!1) {
            return t.some(t=>(function(e, t, n=!1) {
                return !!(0,
                r.HD)(e) && ((0,
                r.Kj)(t) ? t.test(e) : !!(0,
                r.HD)(t) && (n ? e === t : e.includes(t)))
            }
            )(e, t, n))
        }
    },
    96893: function(e, t, n) {
        "use strict";
        n.d(t, {
            $2: function() {
                return a
            },
            WD: function() {
                return s
            },
            cW: function() {
                return l
            }
        });
        var r, i, o = n(67597);
        function s(e) {
            return new l(t=>{
                t(e)
            }
            )
        }
        function a(e) {
            return new l((t,n)=>{
                n(e)
            }
            )
        }
        (r = i || (i = {}))[r.PENDING = 0] = "PENDING",
        r[r.RESOLVED = 1] = "RESOLVED",
        r[r.REJECTED = 2] = "REJECTED";
        class l {
            constructor(e) {
                l.prototype.__init.call(this),
                l.prototype.__init2.call(this),
                l.prototype.__init3.call(this),
                l.prototype.__init4.call(this),
                this._state = i.PENDING,
                this._handlers = [];
                try {
                    e(this._resolve, this._reject)
                } catch (t) {
                    this._reject(t)
                }
            }
            then(e, t) {
                return new l((n,r)=>{
                    this._handlers.push([!1, t=>{
                        if (e)
                            try {
                                n(e(t))
                            } catch (i) {
                                r(i)
                            }
                        else
                            n(t)
                    }
                    , e=>{
                        if (t)
                            try {
                                n(t(e))
                            } catch (i) {
                                r(i)
                            }
                        else
                            r(e)
                    }
                    ]),
                    this._executeHandlers()
                }
                )
            }
            catch(e) {
                return this.then(e=>e, e)
            }
            finally(e) {
                return new l((t,n)=>{
                    let r, i;
                    return this.then(t=>{
                        i = !1,
                        r = t,
                        e && e()
                    }
                    , t=>{
                        i = !0,
                        r = t,
                        e && e()
                    }
                    ).then(()=>{
                        if (i) {
                            n(r);
                            return
                        }
                        t(r)
                    }
                    )
                }
                )
            }
            __init() {
                this._resolve = e=>{
                    this._setResult(i.RESOLVED, e)
                }
            }
            __init2() {
                this._reject = e=>{
                    this._setResult(i.REJECTED, e)
                }
            }
            __init3() {
                this._setResult = (e,t)=>{
                    if (this._state === i.PENDING) {
                        if ((0,
                        o.J8)(t)) {
                            t.then(this._resolve, this._reject);
                            return
                        }
                        this._state = e,
                        this._value = t,
                        this._executeHandlers()
                    }
                }
            }
            __init4() {
                this._executeHandlers = ()=>{
                    if (this._state === i.PENDING)
                        return;
                    let e = this._handlers.slice();
                    this._handlers = [],
                    e.forEach(e=>{
                        e[0] || (this._state === i.RESOLVED && e[1](this._value),
                        this._state === i.REJECTED && e[2](this._value),
                        e[0] = !0)
                    }
                    )
                }
            }
        }
    },
    21170: function(e, t, n) {
        "use strict";
        n.d(t, {
            Z1: function() {
                return d
            },
            ph: function() {
                return c
            },
            yW: function() {
                return u
            }
        });
        var r = n(61422)
          , i = n(71235);
        e = n.hmd(e);
        let o = (0,
        i.Rf)()
          , s = {
            nowSeconds: ()=>Date.now() / 1e3
        }
          , a = (0,
        r.KV)() ? function() {
            try {
                let t = (0,
                r.l$)(e, "perf_hooks");
                return t.performance
            } catch (n) {
                return
            }
        }() : function() {
            let {performance: e} = o;
            if (!e || !e.now)
                return;
            let t = Date.now() - e.now();
            return {
                now: ()=>e.now(),
                timeOrigin: t
            }
        }()
          , l = void 0 === a ? s : {
            nowSeconds: ()=>(a.timeOrigin + a.now()) / 1e3
        }
          , u = s.nowSeconds.bind(s)
          , c = l.nowSeconds.bind(l)
          , d = (()=>{
            let {performance: e} = o;
            if (!e || !e.now)
                return;
            let t = e.now()
              , n = Date.now()
              , r = e.timeOrigin ? Math.abs(e.timeOrigin + t - n) : 36e5
              , i = e.timing && e.timing.navigationStart
              , s = "number" == typeof i ? Math.abs(i + t - n) : 36e5;
            return r < 36e5 || s < 36e5 ? r <= s ? e.timeOrigin : i : n
        }
        )()
    },
    71235: function(e, t, n) {
        "use strict";
        function r(e) {
            return e && e.Math == Math ? e : void 0
        }
        n.d(t, {
            Rf: function() {
                return o
            },
            YO: function() {
                return s
            },
            n2: function() {
                return i
            }
        });
        let i = "object" == typeof globalThis && r(globalThis) || "object" == typeof window && r(window) || "object" == typeof self && r(self) || "object" == typeof n.g && r(n.g) || function() {
            return this
        }() || {};
        function o() {
            return i
        }
        function s(e, t, n) {
            let r = n || i
              , o = r.__SENTRY__ = r.__SENTRY__ || {}
              , s = o[e] || (o[e] = t());
            return s
        }
    },
    27484: function(e) {
        var t, n, r, i, o, s, a, l, u, c, d, p, h, f, g, m, _, y, v, b, S;
        e.exports = (t = "millisecond",
        n = "second",
        r = "minute",
        i = "hour",
        o = "week",
        s = "month",
        a = "quarter",
        l = "year",
        u = "date",
        c = "Invalid Date",
        d = /^(\d{4})[-/]?(\d{1,2})?[-/]?(\d{0,2})[Tt\s]*(\d{1,2})?:?(\d{1,2})?:?(\d{1,2})?[.:]?(\d+)?$/,
        p = /\[([^\]]+)]|Y{1,4}|M{1,4}|D{1,2}|d{1,4}|H{1,2}|h{1,2}|a|A|m{1,2}|s{1,2}|Z{1,2}|SSS/g,
        h = function(e, t, n) {
            var r = String(e);
            return !r || r.length >= t ? e : "" + Array(t + 1 - r.length).join(n) + e
        }
        ,
        (g = {})[f = "en"] = {
            name: "en",
            weekdays: "Sunday_Monday_Tuesday_Wednesday_Thursday_Friday_Saturday".split("_"),
            months: "January_February_March_April_May_June_July_August_September_October_November_December".split("_"),
            ordinal: function(e) {
                var t = ["th", "st", "nd", "rd"]
                  , n = e % 100;
                return "[" + e + (t[(n - 20) % 10] || t[n] || "th") + "]"
            }
        },
        m = function(e) {
            return e instanceof b
        }
        ,
        _ = function e(t, n, r) {
            var i;
            if (!t)
                return f;
            if ("string" == typeof t) {
                var o = t.toLowerCase();
                g[o] && (i = o),
                n && (g[o] = n,
                i = o);
                var s = t.split("-");
                if (!i && s.length > 1)
                    return e(s[0])
            } else {
                var a = t.name;
                g[a] = t,
                i = a
            }
            return !r && i && (f = i),
            i || !r && f
        }
        ,
        y = function(e, t) {
            if (m(e))
                return e.clone();
            var n = "object" == typeof t ? t : {};
            return n.date = e,
            n.args = arguments,
            new b(n)
        }
        ,
        (v = {
            s: h,
            z: function(e) {
                var t = -e.utcOffset()
                  , n = Math.abs(t);
                return (t <= 0 ? "+" : "-") + h(Math.floor(n / 60), 2, "0") + ":" + h(n % 60, 2, "0")
            },
            m: function e(t, n) {
                if (t.date() < n.date())
                    return -e(n, t);
                var r = 12 * (n.year() - t.year()) + (n.month() - t.month())
                  , i = t.clone().add(r, s)
                  , o = n - i < 0
                  , a = t.clone().add(r + (o ? -1 : 1), s);
                return +(-(r + (n - i) / (o ? i - a : a - i)) || 0)
            },
            a: function(e) {
                return e < 0 ? Math.ceil(e) || 0 : Math.floor(e)
            },
            p: function(e) {
                return ({
                    M: s,
                    y: l,
                    w: o,
                    d: "day",
                    D: u,
                    h: i,
                    m: r,
                    s: n,
                    ms: t,
                    Q: a
                })[e] || String(e || "").toLowerCase().replace(/s$/, "")
            },
            u: function(e) {
                return void 0 === e
            }
        }).l = _,
        v.i = m,
        v.w = function(e, t) {
            return y(e, {
                locale: t.$L,
                utc: t.$u,
                x: t.$x,
                $offset: t.$offset
            })
        }
        ,
        S = (b = function() {
            function e(e) {
                this.$L = _(e.locale, null, !0),
                this.parse(e)
            }
            var h = e.prototype;
            return h.parse = function(e) {
                this.$d = function(e) {
                    var t = e.date
                      , n = e.utc;
                    if (null === t)
                        return new Date(NaN);
                    if (v.u(t))
                        return new Date;
                    if (t instanceof Date)
                        return new Date(t);
                    if ("string" == typeof t && !/Z$/i.test(t)) {
                        var r = t.match(d);
                        if (r) {
                            var i = r[2] - 1 || 0
                              , o = (r[7] || "0").substring(0, 3);
                            return n ? new Date(Date.UTC(r[1], i, r[3] || 1, r[4] || 0, r[5] || 0, r[6] || 0, o)) : new Date(r[1],i,r[3] || 1,r[4] || 0,r[5] || 0,r[6] || 0,o)
                        }
                    }
                    return new Date(t)
                }(e),
                this.$x = e.x || {},
                this.init()
            }
            ,
            h.init = function() {
                var e = this.$d;
                this.$y = e.getFullYear(),
                this.$M = e.getMonth(),
                this.$D = e.getDate(),
                this.$W = e.getDay(),
                this.$H = e.getHours(),
                this.$m = e.getMinutes(),
                this.$s = e.getSeconds(),
                this.$ms = e.getMilliseconds()
            }
            ,
            h.$utils = function() {
                return v
            }
            ,
            h.isValid = function() {
                return this.$d.toString() !== c
            }
            ,
            h.isSame = function(e, t) {
                var n = y(e);
                return this.startOf(t) <= n && n <= this.endOf(t)
            }
            ,
            h.isAfter = function(e, t) {
                return y(e) < this.startOf(t)
            }
            ,
            h.isBefore = function(e, t) {
                return this.endOf(t) < y(e)
            }
            ,
            h.$g = function(e, t, n) {
                return v.u(e) ? this[t] : this.set(n, e)
            }
            ,
            h.unix = function() {
                return Math.floor(this.valueOf() / 1e3)
            }
            ,
            h.valueOf = function() {
                return this.$d.getTime()
            }
            ,
            h.startOf = function(e, t) {
                var a = this
                  , c = !!v.u(t) || t
                  , d = v.p(e)
                  , p = function(e, t) {
                    var n = v.w(a.$u ? Date.UTC(a.$y, t, e) : new Date(a.$y,t,e), a);
                    return c ? n : n.endOf("day")
                }
                  , h = function(e, t) {
                    return v.w(a.toDate()[e].apply(a.toDate("s"), (c ? [0, 0, 0, 0] : [23, 59, 59, 999]).slice(t)), a)
                }
                  , f = this.$W
                  , g = this.$M
                  , m = this.$D
                  , _ = "set" + (this.$u ? "UTC" : "");
                switch (d) {
                case l:
                    return c ? p(1, 0) : p(31, 11);
                case s:
                    return c ? p(1, g) : p(0, g + 1);
                case o:
                    var y = this.$locale().weekStart || 0
                      , b = (f < y ? f + 7 : f) - y;
                    return p(c ? m - b : m + (6 - b), g);
                case "day":
                case u:
                    return h(_ + "Hours", 0);
                case i:
                    return h(_ + "Minutes", 1);
                case r:
                    return h(_ + "Seconds", 2);
                case n:
                    return h(_ + "Milliseconds", 3);
                default:
                    return this.clone()
                }
            }
            ,
            h.endOf = function(e) {
                return this.startOf(e, !1)
            }
            ,
            h.$set = function(e, o) {
                var a, c = v.p(e), d = "set" + (this.$u ? "UTC" : ""), p = ((a = {}).day = d + "Date",
                a[u] = d + "Date",
                a[s] = d + "Month",
                a[l] = d + "FullYear",
                a[i] = d + "Hours",
                a[r] = d + "Minutes",
                a[n] = d + "Seconds",
                a[t] = d + "Milliseconds",
                a)[c], h = "day" === c ? this.$D + (o - this.$W) : o;
                if (c === s || c === l) {
                    var f = this.clone().set(u, 1);
                    f.$d[p](h),
                    f.init(),
                    this.$d = f.set(u, Math.min(this.$D, f.daysInMonth())).$d
                } else
                    p && this.$d[p](h);
                return this.init(),
                this
            }
            ,
            h.set = function(e, t) {
                return this.clone().$set(e, t)
            }
            ,
            h.get = function(e) {
                return this[v.p(e)]()
            }
            ,
            h.add = function(e, t) {
                var a, u = this;
                e = Number(e);
                var c = v.p(t)
                  , d = function(t) {
                    var n = y(u);
                    return v.w(n.date(n.date() + Math.round(t * e)), u)
                };
                if (c === s)
                    return this.set(s, this.$M + e);
                if (c === l)
                    return this.set(l, this.$y + e);
                if ("day" === c)
                    return d(1);
                if (c === o)
                    return d(7);
                var p = ((a = {})[r] = 6e4,
                a[i] = 36e5,
                a[n] = 1e3,
                a)[c] || 1
                  , h = this.$d.getTime() + e * p;
                return v.w(h, this)
            }
            ,
            h.subtract = function(e, t) {
                return this.add(-1 * e, t)
            }
            ,
            h.format = function(e) {
                var t = this
                  , n = this.$locale();
                if (!this.isValid())
                    return n.invalidDate || c;
                var r = e || "YYYY-MM-DDTHH:mm:ssZ"
                  , i = v.z(this)
                  , o = this.$H
                  , s = this.$m
                  , a = this.$M
                  , l = n.weekdays
                  , u = n.months
                  , d = n.meridiem
                  , h = function(e, n, i, o) {
                    return e && (e[n] || e(t, r)) || i[n].slice(0, o)
                }
                  , f = function(e) {
                    return v.s(o % 12 || 12, e, "0")
                }
                  , g = d || function(e, t, n) {
                    var r = e < 12 ? "AM" : "PM";
                    return n ? r.toLowerCase() : r
                }
                ;
                return r.replace(p, function(e, r) {
                    return r || function(e) {
                        switch (e) {
                        case "YY":
                            return String(t.$y).slice(-2);
                        case "YYYY":
                            return v.s(t.$y, 4, "0");
                        case "M":
                            return a + 1;
                        case "MM":
                            return v.s(a + 1, 2, "0");
                        case "MMM":
                            return h(n.monthsShort, a, u, 3);
                        case "MMMM":
                            return h(u, a);
                        case "D":
                            return t.$D;
                        case "DD":
                            return v.s(t.$D, 2, "0");
                        case "d":
                            return String(t.$W);
                        case "dd":
                            return h(n.weekdaysMin, t.$W, l, 2);
                        case "ddd":
                            return h(n.weekdaysShort, t.$W, l, 3);
                        case "dddd":
                            return l[t.$W];
                        case "H":
                            return String(o);
                        case "HH":
                            return v.s(o, 2, "0");
                        case "h":
                            return f(1);
                        case "hh":
                            return f(2);
                        case "a":
                            return g(o, s, !0);
                        case "A":
                            return g(o, s, !1);
                        case "m":
                            return String(s);
                        case "mm":
                            return v.s(s, 2, "0");
                        case "s":
                            return String(t.$s);
                        case "ss":
                            return v.s(t.$s, 2, "0");
                        case "SSS":
                            return v.s(t.$ms, 3, "0");
                        case "Z":
                            return i
                        }
                        return null
                    }(e) || i.replace(":", "")
                })
            }
            ,
            h.utcOffset = function() {
                return -(15 * Math.round(this.$d.getTimezoneOffset() / 15))
            }
            ,
            h.diff = function(e, t, u) {
                var c, d = this, p = v.p(t), h = y(e), f = (h.utcOffset() - this.utcOffset()) * 6e4, g = this - h, m = function() {
                    return v.m(d, h)
                };
                switch (p) {
                case l:
                    c = m() / 12;
                    break;
                case s:
                    c = m();
                    break;
                case a:
                    c = m() / 3;
                    break;
                case o:
                    c = (g - f) / 6048e5;
                    break;
                case "day":
                    c = (g - f) / 864e5;
                    break;
                case i:
                    c = g / 36e5;
                    break;
                case r:
                    c = g / 6e4;
                    break;
                case n:
                    c = g / 1e3;
                    break;
                default:
                    c = g
                }
                return u ? c : v.a(c)
            }
            ,
            h.daysInMonth = function() {
                return this.endOf(s).$D
            }
            ,
            h.$locale = function() {
                return g[this.$L]
            }
            ,
            h.locale = function(e, t) {
                if (!e)
                    return this.$L;
                var n = this.clone()
                  , r = _(e, t, !0);
                return r && (n.$L = r),
                n
            }
            ,
            h.clone = function() {
                return v.w(this.$d, this)
            }
            ,
            h.toDate = function() {
                return new Date(this.valueOf())
            }
            ,
            h.toJSON = function() {
                return this.isValid() ? this.toISOString() : null
            }
            ,
            h.toISOString = function() {
                return this.$d.toISOString()
            }
            ,
            h.toString = function() {
                return this.$d.toUTCString()
            }
            ,
            e
        }()).prototype,
        y.prototype = S,
        [["$ms", t], ["$s", n], ["$m", r], ["$H", i], ["$W", "day"], ["$M", s], ["$y", l], ["$D", u]].forEach(function(e) {
            S[e[1]] = function(t) {
                return this.$g(t, e[0], e[1])
            }
        }),
        y.extend = function(e, t) {
            return e.$i || (e(t, b, y),
            e.$i = !0),
            y
        }
        ,
        y.locale = _,
        y.isDayjs = m,
        y.unix = function(e) {
            return y(1e3 * e)
        }
        ,
        y.en = g[f],
        y.Ls = g,
        y.p = {},
        y)
    },
    25054: function(e) {
        e.exports = {
            name: "en",
            weekdays: "Sunday_Monday_Tuesday_Wednesday_Thursday_Friday_Saturday".split("_"),
            months: "January_February_March_April_May_June_July_August_September_October_November_December".split("_"),
            ordinal: function(e) {
                var t = ["th", "st", "nd", "rd"]
                  , n = e % 100;
                return "[" + e + (t[(n - 20) % 10] || t[n] || "th") + "]"
            }
        }
    },
    76831: function(e, t, n) {
        var r, i;
        e.exports = (r = n(27484),
        i = {
            name: "ja",
            weekdays: "日曜日_月曜日_火曜日_水曜日_木曜日_金曜日_土曜日".split("_"),
            weekdaysShort: "日_月_火_水_木_金_土".split("_"),
            weekdaysMin: "日_月_火_水_木_金_土".split("_"),
            months: "1月_2月_3月_4月_5月_6月_7月_8月_9月_10月_11月_12月".split("_"),
            monthsShort: "1月_2月_3月_4月_5月_6月_7月_8月_9月_10月_11月_12月".split("_"),
            ordinal: function(e) {
                return e + "日"
            },
            formats: {
                LT: "HH:mm",
                LTS: "HH:mm:ss",
                L: "YYYY/MM/DD",
                LL: "YYYY年M月D日",
                LLL: "YYYY年M月D日 HH:mm",
                LLLL: "YYYY年M月D日 dddd HH:mm",
                l: "YYYY/MM/DD",
                ll: "YYYY年M月D日",
                lll: "YYYY年M月D日 HH:mm",
                llll: "YYYY年M月D日(ddd) HH:mm"
            },
            meridiem: function(e) {
                return e < 12 ? "午前" : "午後"
            },
            relativeTime: {
                future: "%s後",
                past: "%s前",
                s: "数秒",
                m: "1分",
                mm: "%d分",
                h: "1時間",
                hh: "%d時間",
                d: "1日",
                dd: "%d日",
                M: "1ヶ月",
                MM: "%dヶ月",
                y: "1年",
                yy: "%d年"
            }
        },
        (r && "object" == typeof r && "default"in r ? r : {
            default: r
        }).default.locale(i, null, !0),
        i)
    },
    29387: function(e) {
        var t, n;
        e.exports = (t = {
            year: 0,
            month: 1,
            day: 2,
            hour: 3,
            minute: 4,
            second: 5
        },
        n = {},
        function(e, r, i) {
            var o, s = function(e, t, r) {
                void 0 === r && (r = {});
                var i, o, s, a, l = new Date(e);
                return (void 0 === (i = r) && (i = {}),
                (a = n[s = t + "|" + (o = i.timeZoneName || "short")]) || (a = new Intl.DateTimeFormat("en-US",{
                    hour12: !1,
                    timeZone: t,
                    year: "numeric",
                    month: "2-digit",
                    day: "2-digit",
                    hour: "2-digit",
                    minute: "2-digit",
                    second: "2-digit",
                    timeZoneName: o
                }),
                n[s] = a),
                a).formatToParts(l)
            }, a = function(e, n) {
                for (var r = s(e, n), o = [], a = 0; a < r.length; a += 1) {
                    var l = r[a]
                      , u = l.type
                      , c = l.value
                      , d = t[u];
                    d >= 0 && (o[d] = parseInt(c, 10))
                }
                var p = o[3]
                  , h = o[0] + "-" + o[1] + "-" + o[2] + " " + (24 === p ? 0 : p) + ":" + o[4] + ":" + o[5] + ":000"
                  , f = +e;
                return (i.utc(h).valueOf() - (f -= f % 1e3)) / 6e4
            }, l = r.prototype;
            l.tz = function(e, t) {
                void 0 === e && (e = o);
                var n = this.utcOffset()
                  , r = this.toDate()
                  , s = r.toLocaleString("en-US", {
                    timeZone: e
                })
                  , a = Math.round((r - new Date(s)) / 1e3 / 60)
                  , l = i(s).$set("millisecond", this.$ms).utcOffset(-(15 * Math.round(r.getTimezoneOffset() / 15)) - a, !0);
                if (t) {
                    var u = l.utcOffset();
                    l = l.add(n - u, "minute")
                }
                return l.$x.$timezone = e,
                l
            }
            ,
            l.offsetName = function(e) {
                var t = this.$x.$timezone || i.tz.guess()
                  , n = s(this.valueOf(), t, {
                    timeZoneName: e
                }).find(function(e) {
                    return "timezonename" === e.type.toLowerCase()
                });
                return n && n.value
            }
            ;
            var u = l.startOf;
            l.startOf = function(e, t) {
                if (!this.$x || !this.$x.$timezone)
                    return u.call(this, e, t);
                var n = i(this.format("YYYY-MM-DD HH:mm:ss:SSS"));
                return u.call(n, e, t).tz(this.$x.$timezone, !0)
            }
            ,
            i.tz = function(e, t, n) {
                var r = n || t || o
                  , s = a(+i(), r);
                if ("string" != typeof e)
                    return i(e).tz(r);
                var l = function(e, t, n) {
                    var r = e - 60 * t * 1e3
                      , i = a(r, n);
                    if (t === i)
                        return [r, t];
                    var o = a(r -= 60 * (i - t) * 1e3, n);
                    return i === o ? [r, i] : [e - 60 * Math.min(i, o) * 1e3, Math.max(i, o)]
                }(i.utc(e, n && t).valueOf(), s, r)
                  , u = l[0]
                  , c = l[1]
                  , d = i(u).utcOffset(c);
                return d.$x.$timezone = r,
                d
            }
            ,
            i.tz.guess = function() {
                return Intl.DateTimeFormat().resolvedOptions().timeZone
            }
            ,
            i.tz.setDefault = function(e) {
                o = e
            }
        }
        )
    },
    70178: function(e) {
        var t, n, r;
        e.exports = (t = "minute",
        n = /[+-]\d\d(?::?\d\d)?/g,
        r = /([+-]|\d\d)/g,
        function(e, i, o) {
            var s = i.prototype;
            o.utc = function(e) {
                var t = {
                    date: e,
                    utc: !0,
                    args: arguments
                };
                return new i(t)
            }
            ,
            s.utc = function(e) {
                var n = o(this.toDate(), {
                    locale: this.$L,
                    utc: !0
                });
                return e ? n.add(this.utcOffset(), t) : n
            }
            ,
            s.local = function() {
                return o(this.toDate(), {
                    locale: this.$L,
                    utc: !1
                })
            }
            ;
            var a = s.parse;
            s.parse = function(e) {
                e.utc && (this.$u = !0),
                this.$utils().u(e.$offset) || (this.$offset = e.$offset),
                a.call(this, e)
            }
            ;
            var l = s.init;
            s.init = function() {
                if (this.$u) {
                    var e = this.$d;
                    this.$y = e.getUTCFullYear(),
                    this.$M = e.getUTCMonth(),
                    this.$D = e.getUTCDate(),
                    this.$W = e.getUTCDay(),
                    this.$H = e.getUTCHours(),
                    this.$m = e.getUTCMinutes(),
                    this.$s = e.getUTCSeconds(),
                    this.$ms = e.getUTCMilliseconds()
                } else
                    l.call(this)
            }
            ;
            var u = s.utcOffset;
            s.utcOffset = function(e, i) {
                var o = this.$utils().u;
                if (o(e))
                    return this.$u ? 0 : o(this.$offset) ? u.call(this) : this.$offset;
                if ("string" == typeof e && null === (e = function(e) {
                    void 0 === e && (e = "");
                    var t = e.match(n);
                    if (!t)
                        return null;
                    var i = ("" + t[0]).match(r) || ["-", 0, 0]
                      , o = i[0]
                      , s = 60 * +i[1] + +i[2];
                    return 0 === s ? 0 : "+" === o ? s : -s
                }(e)))
                    return this;
                var s = 16 >= Math.abs(e) ? 60 * e : e
                  , a = this;
                if (i)
                    return a.$offset = s,
                    a.$u = 0 === e,
                    a;
                if (0 !== e) {
                    var l = this.$u ? this.toDate().getTimezoneOffset() : -1 * this.utcOffset();
                    (a = this.local().add(s + l, t)).$offset = s,
                    a.$x.$localOffset = l
                } else
                    a = this.utc();
                return a
            }
            ;
            var c = s.format;
            s.format = function(e) {
                var t = e || (this.$u ? "YYYY-MM-DDTHH:mm:ss[Z]" : "");
                return c.call(this, t)
            }
            ,
            s.valueOf = function() {
                var e = this.$utils().u(this.$offset) ? 0 : this.$offset + (this.$x.$localOffset || this.$d.getTimezoneOffset());
                return this.$d.valueOf() - 6e4 * e
            }
            ,
            s.isUTC = function() {
                return !!this.$u
            }
            ,
            s.toISOString = function() {
                return this.toDate().toISOString()
            }
            ,
            s.toString = function() {
                return this.toDate().toUTCString()
            }
            ;
            var d = s.toDate;
            s.toDate = function(e) {
                return "s" === e && this.$offset ? o(this.format("YYYY-MM-DD HH:mm:ss:SSS")).toDate() : d.call(this)
            }
            ;
            var p = s.diff;
            s.diff = function(e, t, n) {
                if (e && this.$u === e.$u)
                    return p.call(this, e, t, n);
                var r = this.local()
                  , i = o(e).local();
                return p.call(r, i, t, n)
            }
        }
        )
    },
    8679: function(e, t, n) {
        "use strict";
        var r = n(59864)
          , i = {
            childContextTypes: !0,
            contextType: !0,
            contextTypes: !0,
            defaultProps: !0,
            displayName: !0,
            getDefaultProps: !0,
            getDerivedStateFromError: !0,
            getDerivedStateFromProps: !0,
            mixins: !0,
            propTypes: !0,
            type: !0
        }
          , o = {
            name: !0,
            length: !0,
            prototype: !0,
            caller: !0,
            callee: !0,
            arguments: !0,
            arity: !0
        }
          , s = {
            $$typeof: !0,
            compare: !0,
            defaultProps: !0,
            displayName: !0,
            propTypes: !0,
            type: !0
        }
          , a = {};
        function l(e) {
            return r.isMemo(e) ? s : a[e.$$typeof] || i
        }
        a[r.ForwardRef] = {
            $$typeof: !0,
            render: !0,
            defaultProps: !0,
            displayName: !0,
            propTypes: !0
        },
        a[r.Memo] = s;
        var u = Object.defineProperty
          , c = Object.getOwnPropertyNames
          , d = Object.getOwnPropertySymbols
          , p = Object.getOwnPropertyDescriptor
          , h = Object.getPrototypeOf
          , f = Object.prototype;
        e.exports = function e(t, n, r) {
            if ("string" != typeof n) {
                if (f) {
                    var i = h(n);
                    i && i !== f && e(t, i, r)
                }
                var s = c(n);
                d && (s = s.concat(d(n)));
                for (var a = l(t), g = l(n), m = 0; m < s.length; ++m) {
                    var _ = s[m];
                    if (!o[_] && !(r && r[_]) && !(g && g[_]) && !(a && a[_])) {
                        var y = p(n, _);
                        try {
                            u(t, _, y)
                        } catch (v) {}
                    }
                }
            }
            return t
        }
    },
    66337: function() {
        !function() {
            "use strict";
            if ("object" == typeof window) {
                if ("IntersectionObserver"in window && "IntersectionObserverEntry"in window && "intersectionRatio"in window.IntersectionObserverEntry.prototype) {
                    "isIntersecting"in window.IntersectionObserverEntry.prototype || Object.defineProperty(window.IntersectionObserverEntry.prototype, "isIntersecting", {
                        get: function() {
                            return this.intersectionRatio > 0
                        }
                    });
                    return
                }
                var e = window.document
                  , t = []
                  , n = null
                  , r = null;
                o.prototype.THROTTLE_TIMEOUT = 100,
                o.prototype.POLL_INTERVAL = null,
                o.prototype.USE_MUTATION_OBSERVER = !0,
                o._setupCrossOriginUpdater = function() {
                    return n || (n = function(e, n) {
                        r = e && n ? d(e, n) : u(),
                        t.forEach(function(e) {
                            e._checkForIntersections()
                        })
                    }
                    ),
                    n
                }
                ,
                o._resetCrossOriginUpdater = function() {
                    n = null,
                    r = null
                }
                ,
                o.prototype.observe = function(e) {
                    if (!this._observationTargets.some(function(t) {
                        return t.element == e
                    })) {
                        if (!(e && 1 == e.nodeType))
                            throw Error("target must be an Element");
                        this._registerInstance(),
                        this._observationTargets.push({
                            element: e,
                            entry: null
                        }),
                        this._monitorIntersections(e.ownerDocument),
                        this._checkForIntersections()
                    }
                }
                ,
                o.prototype.unobserve = function(e) {
                    this._observationTargets = this._observationTargets.filter(function(t) {
                        return t.element != e
                    }),
                    this._unmonitorIntersections(e.ownerDocument),
                    0 == this._observationTargets.length && this._unregisterInstance()
                }
                ,
                o.prototype.disconnect = function() {
                    this._observationTargets = [],
                    this._unmonitorAllIntersections(),
                    this._unregisterInstance()
                }
                ,
                o.prototype.takeRecords = function() {
                    var e = this._queuedEntries.slice();
                    return this._queuedEntries = [],
                    e
                }
                ,
                o.prototype._initThresholds = function(e) {
                    var t = e || [0];
                    return Array.isArray(t) || (t = [t]),
                    t.sort().filter(function(e, t, n) {
                        if ("number" != typeof e || isNaN(e) || e < 0 || e > 1)
                            throw Error("threshold must be a number between 0 and 1 inclusively");
                        return e !== n[t - 1]
                    })
                }
                ,
                o.prototype._parseRootMargin = function(e) {
                    var t = (e || "0px").split(/\s+/).map(function(e) {
                        var t = /^(-?\d*\.?\d+)(px|%)$/.exec(e);
                        if (!t)
                            throw Error("rootMargin must be specified in pixels or percent");
                        return {
                            value: parseFloat(t[1]),
                            unit: t[2]
                        }
                    });
                    return t[1] = t[1] || t[0],
                    t[2] = t[2] || t[0],
                    t[3] = t[3] || t[1],
                    t
                }
                ,
                o.prototype._monitorIntersections = function(t) {
                    var n = t.defaultView;
                    if (n && -1 == this._monitoringDocuments.indexOf(t)) {
                        var r = this._checkForIntersections
                          , i = null
                          , o = null;
                        if (this.POLL_INTERVAL ? i = n.setInterval(r, this.POLL_INTERVAL) : (s(n, "resize", r, !0),
                        s(t, "scroll", r, !0),
                        this.USE_MUTATION_OBSERVER && "MutationObserver"in n && (o = new n.MutationObserver(r)).observe(t, {
                            attributes: !0,
                            childList: !0,
                            characterData: !0,
                            subtree: !0
                        })),
                        this._monitoringDocuments.push(t),
                        this._monitoringUnsubscribes.push(function() {
                            var e = t.defaultView;
                            e && (i && e.clearInterval(i),
                            a(e, "resize", r, !0)),
                            a(t, "scroll", r, !0),
                            o && o.disconnect()
                        }),
                        t != (this.root && this.root.ownerDocument || e)) {
                            var l = f(t);
                            l && this._monitorIntersections(l.ownerDocument)
                        }
                    }
                }
                ,
                o.prototype._unmonitorIntersections = function(t) {
                    var n = this._monitoringDocuments.indexOf(t);
                    if (-1 != n) {
                        var r = this.root && this.root.ownerDocument || e;
                        if (!this._observationTargets.some(function(e) {
                            var n = e.element.ownerDocument;
                            if (n == t)
                                return !0;
                            for (; n && n != r; ) {
                                var i = f(n);
                                if ((n = i && i.ownerDocument) == t)
                                    return !0
                            }
                            return !1
                        })) {
                            var i = this._monitoringUnsubscribes[n];
                            if (this._monitoringDocuments.splice(n, 1),
                            this._monitoringUnsubscribes.splice(n, 1),
                            i(),
                            t != r) {
                                var o = f(t);
                                o && this._unmonitorIntersections(o.ownerDocument)
                            }
                        }
                    }
                }
                ,
                o.prototype._unmonitorAllIntersections = function() {
                    var e = this._monitoringUnsubscribes.slice(0);
                    this._monitoringDocuments.length = 0,
                    this._monitoringUnsubscribes.length = 0;
                    for (var t = 0; t < e.length; t++)
                        e[t]()
                }
                ,
                o.prototype._checkForIntersections = function() {
                    if (this.root || !n || r) {
                        var e = this._rootIsInDom()
                          , t = e ? this._getRootRect() : u();
                        this._observationTargets.forEach(function(r) {
                            var o = r.element
                              , s = l(o)
                              , a = this._rootContainsTarget(o)
                              , u = r.entry
                              , c = e && a && this._computeTargetAndRootIntersection(o, s, t)
                              , d = r.entry = new i({
                                time: window.performance && performance.now && performance.now(),
                                target: o,
                                boundingClientRect: s,
                                rootBounds: n && !this.root ? null : t,
                                intersectionRect: c
                            });
                            u ? e && a ? this._hasCrossedThreshold(u, d) && this._queuedEntries.push(d) : u && u.isIntersecting && this._queuedEntries.push(d) : this._queuedEntries.push(d)
                        }, this),
                        this._queuedEntries.length && this._callback(this.takeRecords(), this)
                    }
                }
                ,
                o.prototype._computeTargetAndRootIntersection = function(t, i, o) {
                    if ("none" != window.getComputedStyle(t).display) {
                        for (var s = i, a = h(t), u = !1; !u && a; ) {
                            var c = null
                              , p = 1 == a.nodeType ? window.getComputedStyle(a) : {};
                            if ("none" == p.display)
                                return null;
                            if (a == this.root || 9 == a.nodeType) {
                                if (u = !0,
                                a == this.root || a == e)
                                    n && !this.root ? r && (0 != r.width || 0 != r.height) ? c = r : (a = null,
                                    c = null,
                                    s = null) : c = o;
                                else {
                                    var f = h(a)
                                      , g = f && l(f)
                                      , m = f && this._computeTargetAndRootIntersection(f, g, o);
                                    g && m ? (a = f,
                                    c = d(g, m)) : (a = null,
                                    s = null)
                                }
                            } else {
                                var _ = a.ownerDocument;
                                a != _.body && a != _.documentElement && "visible" != p.overflow && (c = l(a))
                            }
                            if (c && (s = function(e, t) {
                                var n = Math.max(e.top, t.top)
                                  , r = Math.min(e.bottom, t.bottom)
                                  , i = Math.max(e.left, t.left)
                                  , o = Math.min(e.right, t.right)
                                  , s = o - i
                                  , a = r - n;
                                return s >= 0 && a >= 0 && {
                                    top: n,
                                    bottom: r,
                                    left: i,
                                    right: o,
                                    width: s,
                                    height: a
                                } || null
                            }(c, s)),
                            !s)
                                break;
                            a = a && h(a)
                        }
                        return s
                    }
                }
                ,
                o.prototype._getRootRect = function() {
                    var t;
                    if (this.root)
                        t = l(this.root);
                    else {
                        var n = e.documentElement
                          , r = e.body;
                        t = {
                            top: 0,
                            left: 0,
                            right: n.clientWidth || r.clientWidth,
                            width: n.clientWidth || r.clientWidth,
                            bottom: n.clientHeight || r.clientHeight,
                            height: n.clientHeight || r.clientHeight
                        }
                    }
                    return this._expandRectByRootMargin(t)
                }
                ,
                o.prototype._expandRectByRootMargin = function(e) {
                    var t = this._rootMarginValues.map(function(t, n) {
                        return "px" == t.unit ? t.value : t.value * (n % 2 ? e.width : e.height) / 100
                    })
                      , n = {
                        top: e.top - t[0],
                        right: e.right + t[1],
                        bottom: e.bottom + t[2],
                        left: e.left - t[3]
                    };
                    return n.width = n.right - n.left,
                    n.height = n.bottom - n.top,
                    n
                }
                ,
                o.prototype._hasCrossedThreshold = function(e, t) {
                    var n = e && e.isIntersecting ? e.intersectionRatio || 0 : -1
                      , r = t.isIntersecting ? t.intersectionRatio || 0 : -1;
                    if (n !== r)
                        for (var i = 0; i < this.thresholds.length; i++) {
                            var o = this.thresholds[i];
                            if (o == n || o == r || o < n != o < r)
                                return !0
                        }
                }
                ,
                o.prototype._rootIsInDom = function() {
                    return !this.root || p(e, this.root)
                }
                ,
                o.prototype._rootContainsTarget = function(t) {
                    return p(this.root || e, t) && (!this.root || this.root.ownerDocument == t.ownerDocument)
                }
                ,
                o.prototype._registerInstance = function() {
                    0 > t.indexOf(this) && t.push(this)
                }
                ,
                o.prototype._unregisterInstance = function() {
                    var e = t.indexOf(this);
                    -1 != e && t.splice(e, 1)
                }
                ,
                window.IntersectionObserver = o,
                window.IntersectionObserverEntry = i
            }
            function i(e) {
                this.time = e.time,
                this.target = e.target,
                this.rootBounds = c(e.rootBounds),
                this.boundingClientRect = c(e.boundingClientRect),
                this.intersectionRect = c(e.intersectionRect || u()),
                this.isIntersecting = !!e.intersectionRect;
                var t = this.boundingClientRect
                  , n = t.width * t.height
                  , r = this.intersectionRect
                  , i = r.width * r.height;
                n ? this.intersectionRatio = Number((i / n).toFixed(4)) : this.intersectionRatio = this.isIntersecting ? 1 : 0
            }
            function o(e, t) {
                var n, r, i, o = t || {};
                if ("function" != typeof e)
                    throw Error("callback must be a function");
                if (o.root && 1 != o.root.nodeType)
                    throw Error("root must be an Element");
                this._checkForIntersections = (n = this._checkForIntersections.bind(this),
                r = this.THROTTLE_TIMEOUT,
                i = null,
                function() {
                    i || (i = setTimeout(function() {
                        n(),
                        i = null
                    }, r))
                }
                ),
                this._callback = e,
                this._observationTargets = [],
                this._queuedEntries = [],
                this._rootMarginValues = this._parseRootMargin(o.rootMargin),
                this.thresholds = this._initThresholds(o.threshold),
                this.root = o.root || null,
                this.rootMargin = this._rootMarginValues.map(function(e) {
                    return e.value + e.unit
                }).join(" "),
                this._monitoringDocuments = [],
                this._monitoringUnsubscribes = []
            }
            function s(e, t, n, r) {
                "function" == typeof e.addEventListener ? e.addEventListener(t, n, r || !1) : "function" == typeof e.attachEvent && e.attachEvent("on" + t, n)
            }
            function a(e, t, n, r) {
                "function" == typeof e.removeEventListener ? e.removeEventListener(t, n, r || !1) : "function" == typeof e.detatchEvent && e.detatchEvent("on" + t, n)
            }
            function l(e) {
                var t;
                try {
                    t = e.getBoundingClientRect()
                } catch (n) {}
                return t ? (t.width && t.height || (t = {
                    top: t.top,
                    right: t.right,
                    bottom: t.bottom,
                    left: t.left,
                    width: t.right - t.left,
                    height: t.bottom - t.top
                }),
                t) : u()
            }
            function u() {
                return {
                    top: 0,
                    bottom: 0,
                    left: 0,
                    right: 0,
                    width: 0,
                    height: 0
                }
            }
            function c(e) {
                return !e || "x"in e ? e : {
                    top: e.top,
                    y: e.top,
                    bottom: e.bottom,
                    left: e.left,
                    x: e.left,
                    right: e.right,
                    width: e.width,
                    height: e.height
                }
            }
            function d(e, t) {
                var n = t.top - e.top
                  , r = t.left - e.left;
                return {
                    top: n,
                    left: r,
                    height: t.height,
                    width: t.width,
                    bottom: n + t.height,
                    right: r + t.width
                }
            }
            function p(e, t) {
                for (var n = t; n; ) {
                    if (n == e)
                        return !0;
                    n = h(n)
                }
                return !1
            }
            function h(t) {
                var n = t.parentNode;
                return 9 == t.nodeType && t != e ? f(t) : n && 11 == n.nodeType && n.host ? n.host : n && n.assignedSlot ? n.assignedSlot.parentNode : n
            }
            function f(e) {
                try {
                    return e.defaultView && e.defaultView.frameElement || null
                } catch (t) {
                    return null
                }
            }
        }()
    },
    6840: function(e, t, n) {
        (window.__NEXT_P = window.__NEXT_P || []).push(["/_app", function() {
            return n(16560)
        }
        ])
    },
    54314: function(e, t, n) {
        "use strict";
        let r, i, o, s, a, l, u, c, d;
        var p, h, f, g = n(95659);
        function m(e) {
            if ("boolean" == typeof __SENTRY_TRACING__ && !__SENTRY_TRACING__)
                return !1;
            let t = (0,
            g.Gd)().getClient()
              , n = e || t && t.getOptions();
            return !!n && (n.enableTracing || "tracesSampleRate"in n || "tracesSampler"in n)
        }
        let _ = /^(\S+:\\|\/?)([\s\S]*?)((?:\.{1,2}|[^/\\]+?|)(\.[^./\\]*|))(?:[/\\]*)$/;
        function y(...e) {
            let t = ""
              , n = !1;
            for (let r = e.length - 1; r >= -1 && !n; r--) {
                let i = r >= 0 ? e[r] : "/";
                i && (t = `${i}/${t}`,
                n = "/" === i.charAt(0))
            }
            return t = (function(e, t) {
                let n = 0;
                for (let r = e.length - 1; r >= 0; r--) {
                    let i = e[r];
                    "." === i ? e.splice(r, 1) : ".." === i ? (e.splice(r, 1),
                    n++) : n && (e.splice(r, 1),
                    n--)
                }
                if (t)
                    for (; n--; n)
                        e.unshift("..");
                return e
            }
            )(t.split("/").filter(e=>!!e), !n).join("/"),
            (n ? "/" : "") + t || "."
        }
        function v(e) {
            let t = 0;
            for (; t < e.length && "" === e[t]; t++)
                ;
            let n = e.length - 1;
            for (; n >= 0 && "" === e[n]; n--)
                ;
            return t > n ? [] : e.slice(t, n - t + 1)
        }
        class b {
            static __initStatic() {
                this.id = "RewriteFrames"
            }
            constructor(e={}) {
                b.prototype.__init.call(this),
                this.name = b.id,
                e.root && (this._root = e.root),
                this._prefix = e.prefix || "app:///",
                e.iteratee && (this._iteratee = e.iteratee)
            }
            setupOnce(e, t) {
                e(e=>{
                    let n = t().getIntegration(b);
                    return n ? n.process(e) : e
                }
                )
            }
            process(e) {
                let t = e;
                return e.exception && Array.isArray(e.exception.values) && (t = this._processExceptionsEvent(t)),
                t
            }
            __init() {
                this._iteratee = e=>{
                    if (!e.filename)
                        return e;
                    let t = /^[a-zA-Z]:\\/.test(e.filename) || e.filename.includes("\\") && !e.filename.includes("/")
                      , n = /^\//.test(e.filename);
                    if (t || n) {
                        var r;
                        let i;
                        let o = t ? e.filename.replace(/^[a-zA-Z]:/, "").replace(/\\/g, "/") : e.filename
                          , s = this._root ? function(e, t) {
                            e = y(e).slice(1),
                            t = y(t).slice(1);
                            let n = v(e.split("/"))
                              , r = v(t.split("/"))
                              , i = Math.min(n.length, r.length)
                              , o = i;
                            for (let s = 0; s < i; s++)
                                if (n[s] !== r[s]) {
                                    o = s;
                                    break
                                }
                            let a = [];
                            for (let l = o; l < n.length; l++)
                                a.push("..");
                            return (a = a.concat(r.slice(o))).join("/")
                        }(this._root, o) : (i = function(e) {
                            let t = e.length > 1024 ? `<truncated>${e.slice(-1024)}` : e
                              , n = _.exec(t);
                            return n ? n.slice(1) : []
                        }(o)[2],
                        r && i.slice(-1 * r.length) === r && (i = i.slice(0, i.length - r.length)),
                        i);
                        e.filename = `${this._prefix}${s}`
                    }
                    return e
                }
            }
            _processExceptionsEvent(e) {
                try {
                    return {
                        ...e,
                        exception: {
                            ...e.exception,
                            values: e.exception.values.map(e=>({
                                ...e,
                                ...e.stacktrace && {
                                    stacktrace: this._processStacktrace(e.stacktrace)
                                }
                            }))
                        }
                    }
                } catch (t) {
                    return e
                }
            }
            _processStacktrace(e) {
                return {
                    ...e,
                    frames: e && e.frames && e.frames.map(e=>this._iteratee(e))
                }
            }
        }
        b.__initStatic();
        let S = "7.64.0";
        var E = n(12343)
          , w = n(62844)
          , x = n(57321);
        let T = [/^Script error\.?$/, /^Javascript error: Script error\.? on line 0$/]
          , k = [/^.*healthcheck.*$/, /^.*healthy.*$/, /^.*live.*$/, /^.*ready.*$/, /^.*heartbeat.*$/, /^.*\/health$/, /^.*\/healthz$/];
        class R {
            static __initStatic() {
                this.id = "InboundFilters"
            }
            constructor(e={}) {
                this.name = R.id,
                this._options = e
            }
            setupOnce(e, t) {
                let n = e=>{
                    let n = t();
                    if (n) {
                        let r = n.getIntegration(R);
                        if (r) {
                            var i;
                            let o = n.getClient()
                              , s = o ? o.getOptions() : {}
                              , a = function(e={}, t={}) {
                                return {
                                    allowUrls: [...e.allowUrls || [], ...t.allowUrls || []],
                                    denyUrls: [...e.denyUrls || [], ...t.denyUrls || []],
                                    ignoreErrors: [...e.ignoreErrors || [], ...t.ignoreErrors || [], ...e.disableErrorDefaults ? [] : T],
                                    ignoreTransactions: [...e.ignoreTransactions || [], ...t.ignoreTransactions || [], ...e.disableTransactionDefaults ? [] : k],
                                    ignoreInternal: void 0 === e.ignoreInternal || e.ignoreInternal
                                }
                            }(r._options, s);
                            return (a.ignoreInternal && function(e) {
                                try {
                                    return "SentryError" === e.exception.values[0].type
                                } catch (t) {}
                                return !1
                            }(e) ? (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`Event dropped due to being internal Sentry Error.
Event: ${(0,
                            w.jH)(e)}`),
                            0) : (i = a.ignoreErrors,
                            !e.type && i && i.length && (function(e) {
                                if (e.message)
                                    return [e.message];
                                if (e.exception) {
                                    let {values: t} = e.exception;
                                    try {
                                        let {type: n="", value: r=""} = t && t[t.length - 1] || {};
                                        return [`${r}`, `${n}: ${r}`]
                                    } catch (i) {
                                        ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.error(`Cannot extract message for event ${(0,
                                        w.jH)(e)}`)
                                    }
                                }
                                return []
                            }
                            )(e).some(e=>(0,
                            x.U0)(e, i))) ? (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`Event dropped due to being matched by \`ignoreErrors\` option.
Event: ${(0,
                            w.jH)(e)}`),
                            0) : !function(e, t) {
                                if ("transaction" !== e.type || !t || !t.length)
                                    return !1;
                                let n = e.transaction;
                                return !!n && (0,
                                x.U0)(n, t)
                            }(e, a.ignoreTransactions) ? !function(e, t) {
                                if (!t || !t.length)
                                    return !1;
                                let n = D(e);
                                return !!n && (0,
                                x.U0)(n, t)
                            }(e, a.denyUrls) ? function(e, t) {
                                if (!t || !t.length)
                                    return !0;
                                let n = D(e);
                                return !n || (0,
                                x.U0)(n, t)
                            }(e, a.allowUrls) || (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`Event dropped due to not being matched by \`allowUrls\` option.
Event: ${(0,
                            w.jH)(e)}.
Url: ${D(e)}`),
                            0) : (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`Event dropped due to being matched by \`denyUrls\` option.
Event: ${(0,
                            w.jH)(e)}.
Url: ${D(e)}`),
                            0) : (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`Event dropped due to being matched by \`ignoreTransactions\` option.
Event: ${(0,
                            w.jH)(e)}`),
                            0)) ? e : null
                        }
                    }
                    return e
                }
                ;
                n.id = this.name,
                e(n)
            }
        }
        function D(e) {
            try {
                let t;
                try {
                    t = e.exception.values[0].stacktrace.frames
                } catch (n) {}
                return t ? function(e=[]) {
                    for (let t = e.length - 1; t >= 0; t--) {
                        let n = e[t];
                        if (n && "<anonymous>" !== n.filename && "[native code]" !== n.filename)
                            return n.filename || null
                    }
                    return null
                }(t) : null
            } catch (r) {
                return ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.error(`Cannot extract url for event ${(0,
                w.jH)(e)}`),
                null
            }
        }
        R.__initStatic();
        var O = n(20535);
        class N {
            static __initStatic() {
                this.id = "FunctionToString"
            }
            constructor() {
                this.name = N.id
            }
            setupOnce() {
                r = Function.prototype.toString;
                try {
                    Function.prototype.toString = function(...e) {
                        let t = (0,
                        O.HK)(this) || this;
                        return r.apply(t, e)
                    }
                } catch (e) {}
            }
        }
        N.__initStatic();
        var C = n(10350);
        let $ = [];
        function I(e, t) {
            t[e.name] = e,
            -1 === $.indexOf(e.name) && (e.setupOnce(C.c, g.Gd),
            $.push(e.name),
            ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`Integration installed: ${e.name}`))
        }
        let P = /\(error: (.*)\)/
          , A = /captureMessage|captureException/;
        function L(...e) {
            let t = e.sort((e,t)=>e[0] - t[0]).map(e=>e[1]);
            return (e,n=0)=>{
                let r = []
                  , i = e.split("\n");
                for (let o = n; o < i.length; o++) {
                    let s = i[o];
                    if (s.length > 1024)
                        continue;
                    let a = P.test(s) ? s.replace(P, "$1") : s;
                    if (!a.match(/\S*Error: /)) {
                        for (let l of t) {
                            let u = l(a);
                            if (u) {
                                r.push(u);
                                break
                            }
                        }
                        if (r.length >= 50)
                            break
                    }
                }
                return function(e) {
                    if (!e.length)
                        return [];
                    let t = Array.from(e);
                    return /sentryWrapped/.test(t[t.length - 1].function || "") && t.pop(),
                    t.reverse(),
                    A.test(t[t.length - 1].function || "") && (t.pop(),
                    A.test(t[t.length - 1].function || "") && t.pop()),
                    t.slice(0, 50).map(e=>({
                        ...e,
                        filename: e.filename || t[t.length - 1].filename,
                        function: e.function || "?"
                    }))
                }(r)
            }
        }
        let U = "<anonymous>";
        function j(e) {
            try {
                if (!e || "function" != typeof e)
                    return U;
                return e.name || U
            } catch (t) {
                return U
            }
        }
        var B = n(71235);
        let Y = (0,
        B.Rf)();
        function M() {
            if (!("fetch"in Y))
                return !1;
            try {
                return new Headers,
                new Request("http://www.example.com"),
                new Response,
                !0
            } catch (e) {
                return !1
            }
        }
        function G(e) {
            return e && /^function fetch\(\)\s+\{\s+\[native code\]\s+\}$/.test(e.toString())
        }
        var V = n(67597);
        let H = (0,
        B.Rf)()
          , F = (0,
        B.Rf)()
          , z = "__sentry_xhr_v2__"
          , q = {}
          , W = {};
        function J(e, t) {
            q[e] = q[e] || [],
            q[e].push(t),
            function(e) {
                if (!W[e])
                    switch (W[e] = !0,
                    e) {
                    case "console":
                        "console"in F && E.RU.forEach(function(e) {
                            e in F.console && (0,
                            O.hl)(F.console, e, function(t) {
                                return function(...n) {
                                    K("console", {
                                        args: n,
                                        level: e
                                    }),
                                    t && t.apply(F.console, n)
                                }
                            })
                        });
                        break;
                    case "dom":
                        (function() {
                            if (!("document"in F))
                                return;
                            let e = K.bind(null, "dom")
                              , t = Q(e, !0);
                            F.document.addEventListener("click", t, !1),
                            F.document.addEventListener("keypress", t, !1),
                            ["EventTarget", "Node"].forEach(t=>{
                                let n = F[t] && F[t].prototype;
                                n && n.hasOwnProperty && n.hasOwnProperty("addEventListener") && ((0,
                                O.hl)(n, "addEventListener", function(t) {
                                    return function(n, r, i) {
                                        if ("click" === n || "keypress" == n)
                                            try {
                                                let o = this
                                                  , s = o.__sentry_instrumentation_handlers__ = o.__sentry_instrumentation_handlers__ || {}
                                                  , a = s[n] = s[n] || {
                                                    refCount: 0
                                                };
                                                if (!a.handler) {
                                                    let l = Q(e);
                                                    a.handler = l,
                                                    t.call(this, n, l, i)
                                                }
                                                a.refCount++
                                            } catch (u) {}
                                        return t.call(this, n, r, i)
                                    }
                                }),
                                (0,
                                O.hl)(n, "removeEventListener", function(e) {
                                    return function(t, n, r) {
                                        if ("click" === t || "keypress" == t)
                                            try {
                                                let i = this.__sentry_instrumentation_handlers__ || {}
                                                  , o = i[t];
                                                o && (o.refCount--,
                                                o.refCount <= 0 && (e.call(this, t, o.handler, r),
                                                o.handler = void 0,
                                                delete i[t]),
                                                0 === Object.keys(i).length && delete this.__sentry_instrumentation_handlers__)
                                            } catch (s) {}
                                        return e.call(this, t, n, r)
                                    }
                                }))
                            }
                            )
                        }
                        )();
                        break;
                    case "xhr":
                        (function() {
                            if (!("XMLHttpRequest"in F))
                                return;
                            let e = XMLHttpRequest.prototype;
                            (0,
                            O.hl)(e, "open", function(e) {
                                return function(...t) {
                                    let n = t[1]
                                      , r = this[z] = {
                                        method: (0,
                                        V.HD)(t[0]) ? t[0].toUpperCase() : t[0],
                                        url: t[1],
                                        request_headers: {}
                                    };
                                    (0,
                                    V.HD)(n) && "POST" === r.method && n.match(/sentry_key/) && (this.__sentry_own_request__ = !0);
                                    let i = ()=>{
                                        let e = this[z];
                                        if (e && 4 === this.readyState) {
                                            try {
                                                e.status_code = this.status
                                            } catch (n) {}
                                            K("xhr", {
                                                args: t,
                                                endTimestamp: Date.now(),
                                                startTimestamp: Date.now(),
                                                xhr: this
                                            })
                                        }
                                    }
                                    ;
                                    return "onreadystatechange"in this && "function" == typeof this.onreadystatechange ? (0,
                                    O.hl)(this, "onreadystatechange", function(e) {
                                        return function(...t) {
                                            return i(),
                                            e.apply(this, t)
                                        }
                                    }) : this.addEventListener("readystatechange", i),
                                    (0,
                                    O.hl)(this, "setRequestHeader", function(e) {
                                        return function(...t) {
                                            let[n,r] = t
                                              , i = this[z];
                                            return i && (i.request_headers[n.toLowerCase()] = r),
                                            e.apply(this, t)
                                        }
                                    }),
                                    e.apply(this, t)
                                }
                            }),
                            (0,
                            O.hl)(e, "send", function(e) {
                                return function(...t) {
                                    let n = this[z];
                                    return n && void 0 !== t[0] && (n.body = t[0]),
                                    K("xhr", {
                                        args: t,
                                        startTimestamp: Date.now(),
                                        xhr: this
                                    }),
                                    e.apply(this, t)
                                }
                            })
                        }
                        )();
                        break;
                    case "fetch":
                        !function() {
                            if (!M())
                                return !1;
                            if (G(Y.fetch))
                                return !0;
                            let e = !1
                              , t = Y.document;
                            if (t && "function" == typeof t.createElement)
                                try {
                                    let n = t.createElement("iframe");
                                    n.hidden = !0,
                                    t.head.appendChild(n),
                                    n.contentWindow && n.contentWindow.fetch && (e = G(n.contentWindow.fetch)),
                                    t.head.removeChild(n)
                                } catch (r) {
                                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("Could not create sandbox iframe for pure fetch check, bailing to window.fetch: ", r)
                                }
                            return e
                        }() || (0,
                        O.hl)(F, "fetch", function(e) {
                            return function(...t) {
                                let {method: n, url: r} = function(e) {
                                    if (0 === e.length)
                                        return {
                                            method: "GET",
                                            url: ""
                                        };
                                    if (2 === e.length) {
                                        let[t,n] = e;
                                        return {
                                            url: Z(t),
                                            method: X(n, "method") ? String(n.method).toUpperCase() : "GET"
                                        }
                                    }
                                    let r = e[0];
                                    return {
                                        url: Z(r),
                                        method: X(r, "method") ? String(r.method).toUpperCase() : "GET"
                                    }
                                }(t)
                                  , i = {
                                    args: t,
                                    fetchData: {
                                        method: n,
                                        url: r
                                    },
                                    startTimestamp: Date.now()
                                };
                                return K("fetch", {
                                    ...i
                                }),
                                e.apply(F, t).then(e=>(K("fetch", {
                                    ...i,
                                    endTimestamp: Date.now(),
                                    response: e
                                }),
                                e), e=>{
                                    throw K("fetch", {
                                        ...i,
                                        endTimestamp: Date.now(),
                                        error: e
                                    }),
                                    e
                                }
                                )
                            }
                        });
                        break;
                    case "history":
                        (function() {
                            if (!function() {
                                let e = H.chrome
                                  , t = e && e.app && e.app.runtime
                                  , n = "history"in H && !!H.history.pushState && !!H.history.replaceState;
                                return !t && n
                            }())
                                return;
                            let e = F.onpopstate;
                            function t(e) {
                                return function(...t) {
                                    let n = t.length > 2 ? t[2] : void 0;
                                    if (n) {
                                        let r = i
                                          , o = String(n);
                                        i = o,
                                        K("history", {
                                            from: r,
                                            to: o
                                        })
                                    }
                                    return e.apply(this, t)
                                }
                            }
                            F.onpopstate = function(...t) {
                                let n = F.location.href
                                  , r = i;
                                if (i = n,
                                K("history", {
                                    from: r,
                                    to: n
                                }),
                                e)
                                    try {
                                        return e.apply(this, t)
                                    } catch (o) {}
                            }
                            ,
                            (0,
                            O.hl)(F.history, "pushState", t),
                            (0,
                            O.hl)(F.history, "replaceState", t)
                        }
                        )();
                        break;
                    case "error":
                        ee = F.onerror,
                        F.onerror = function(e, t, n, r, i) {
                            return K("error", {
                                column: r,
                                error: i,
                                line: n,
                                msg: e,
                                url: t
                            }),
                            !!ee && !ee.__SENTRY_LOADER__ && ee.apply(this, arguments)
                        }
                        ,
                        F.onerror.__SENTRY_INSTRUMENTED__ = !0;
                        break;
                    case "unhandledrejection":
                        et = F.onunhandledrejection,
                        F.onunhandledrejection = function(e) {
                            return K("unhandledrejection", e),
                            !et || !!et.__SENTRY_LOADER__ || et.apply(this, arguments)
                        }
                        ,
                        F.onunhandledrejection.__SENTRY_INSTRUMENTED__ = !0;
                        break;
                    default:
                        ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("unknown instrumentation type:", e);
                        return
                    }
            }(e)
        }
        function K(e, t) {
            if (e && q[e])
                for (let n of q[e] || [])
                    try {
                        n(t)
                    } catch (r) {
                        ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.error(`Error while triggering instrumentation handler.
Type: ${e}
Name: ${j(n)}
Error:`, r)
                    }
        }
        function X(e, t) {
            return !!e && "object" == typeof e && !!e[t]
        }
        function Z(e) {
            return "string" == typeof e ? e : e ? X(e, "url") ? e.url : e.toString ? e.toString() : "" : ""
        }
        function Q(e, t=!1) {
            return n=>{
                if (!n || s === n || function(e) {
                    if ("keypress" !== e.type)
                        return !1;
                    try {
                        let t = e.target;
                        if (!t || !t.tagName)
                            return !0;
                        if ("INPUT" === t.tagName || "TEXTAREA" === t.tagName || t.isContentEditable)
                            return !1
                    } catch (n) {}
                    return !0
                }(n))
                    return;
                let r = "keypress" === n.type ? "input" : n.type;
                void 0 === o ? (e({
                    event: n,
                    name: r,
                    global: t
                }),
                s = n) : function(e, t) {
                    if (!e || e.type !== t.type)
                        return !0;
                    try {
                        if (e.target !== t.target)
                            return !0
                    } catch (n) {}
                    return !1
                }(s, n) && (e({
                    event: n,
                    name: r,
                    global: t
                }),
                s = n),
                clearTimeout(o),
                o = F.setTimeout(()=>{
                    o = void 0
                }
                , 1e3)
            }
        }
        let ee = null
          , et = null
          , en = /^(?:(\w+):)\/\/(?:(\w+)(?::(\w+)?)?@)([\w.-]+)(?::(\d+))?\/(.+)/;
        function er(e, t=!1) {
            let {host: n, path: r, pass: i, port: o, projectId: s, protocol: a, publicKey: l} = e;
            return `${a}://${l}${t && i ? `:${i}` : ""}@${n}${o ? `:${o}` : ""}/${r ? `${r}/` : r}${s}`
        }
        function ei(e) {
            let t = en.exec(e);
            if (!t) {
                console.error(`Invalid Sentry Dsn: ${e}`);
                return
            }
            let[n,r,i="",o,s="",a] = t.slice(1)
              , l = ""
              , u = a
              , c = u.split("/");
            if (c.length > 1 && (l = c.slice(0, -1).join("/"),
            u = c.pop()),
            u) {
                let d = u.match(/^\d+/);
                d && (u = d[0])
            }
            return eo({
                host: o,
                pass: i,
                path: l,
                projectId: u,
                port: s,
                protocol: n,
                publicKey: r
            })
        }
        function eo(e) {
            return {
                protocol: e.protocol,
                publicKey: e.publicKey || "",
                pass: e.pass || "",
                host: e.host,
                port: e.port || "",
                path: e.path || "",
                projectId: e.projectId
            }
        }
        var es = n(96893);
        function ea(e, t=100, r=Infinity) {
            try {
                return function e(t, r, i=Infinity, o=Infinity, s=function() {
                    let e = "function" == typeof WeakSet
                      , t = e ? new WeakSet : [];
                    return [function(n) {
                        if (e)
                            return !!t.has(n) || (t.add(n),
                            !1);
                        for (let r = 0; r < t.length; r++) {
                            let i = t[r];
                            if (i === n)
                                return !0
                        }
                        return t.push(n),
                        !1
                    }
                    , function(n) {
                        if (e)
                            t.delete(n);
                        else
                            for (let r = 0; r < t.length; r++)
                                if (t[r] === n) {
                                    t.splice(r, 1);
                                    break
                                }
                    }
                    ]
                }()) {
                    let[a,l] = s;
                    if (null == r || ["number", "boolean", "string"].includes(typeof r) && !(0,
                    V.i2)(r))
                        return r;
                    let u = function(e, t) {
                        try {
                            if ("domain" === e && t && "object" == typeof t && t._events)
                                return "[Domain]";
                            if ("domainEmitter" === e)
                                return "[DomainEmitter]";
                            if (void 0 !== n.g && t === n.g)
                                return "[Global]";
                            if ("undefined" != typeof window && t === window)
                                return "[Window]";
                            if ("undefined" != typeof document && t === document)
                                return "[Document]";
                            if ((0,
                            V.Cy)(t))
                                return "[SyntheticEvent]";
                            if ("number" == typeof t && t != t)
                                return "[NaN]";
                            if ("function" == typeof t)
                                return `[Function: ${j(t)}]`;
                            if ("symbol" == typeof t)
                                return `[${String(t)}]`;
                            if ("bigint" == typeof t)
                                return `[BigInt: ${String(t)}]`;
                            let r = function(e) {
                                let t = Object.getPrototypeOf(e);
                                return t ? t.constructor.name : "null prototype"
                            }(t);
                            if (/^HTML(\w*)Element$/.test(r))
                                return `[HTMLElement: ${r}]`;
                            return `[object ${r}]`
                        } catch (i) {
                            return `**non-serializable** (${i})`
                        }
                    }(t, r);
                    if (!u.startsWith("[object "))
                        return u;
                    if (r.__sentry_skip_normalization__)
                        return r;
                    let c = "number" == typeof r.__sentry_override_normalization_depth__ ? r.__sentry_override_normalization_depth__ : i;
                    if (0 === c)
                        return u.replace("object ", "");
                    if (a(r))
                        return "[Circular ~]";
                    if (r && "function" == typeof r.toJSON)
                        try {
                            let d = r.toJSON();
                            return e("", d, c - 1, o, s)
                        } catch (p) {}
                    let h = Array.isArray(r) ? [] : {}
                      , f = 0
                      , g = (0,
                    O.Sh)(r);
                    for (let m in g) {
                        if (!Object.prototype.hasOwnProperty.call(g, m))
                            continue;
                        if (f >= o) {
                            h[m] = "[MaxProperties ~]";
                            break
                        }
                        let _ = g[m];
                        h[m] = e(m, _, c - 1, o, s),
                        f++
                    }
                    return l(r),
                    h
                }("", e, t, r)
            } catch (i) {
                return {
                    ERROR: `**non-serializable** (${i})`
                }
            }
        }
        function el(e, t=[]) {
            return [e, t]
        }
        function eu(e, t) {
            let n = e[1];
            for (let r of n) {
                let i = r[0].type
                  , o = t(r, i);
                if (o)
                    return !0
            }
            return !1
        }
        function ec(e, t) {
            let n = t || new TextEncoder;
            return n.encode(e)
        }
        let ed = {
            session: "session",
            sessions: "session",
            attachment: "attachment",
            transaction: "transaction",
            event: "error",
            client_report: "internal",
            user_report: "default",
            profile: "profile",
            replay_event: "replay",
            replay_recording: "replay",
            check_in: "monitor"
        };
        function ep(e) {
            if (!e || !e.sdk)
                return;
            let {name: t, version: n} = e.sdk;
            return {
                name: t,
                version: n
            }
        }
        class eh extends Error {
            constructor(e, t="warn") {
                super(e),
                this.message = e,
                this.name = new.target.prototype.constructor.name,
                Object.setPrototypeOf(this, new.target.prototype),
                this.logLevel = t
            }
        }
        var ef = n(9015)
          , eg = n(51131);
        function em(e, t, n) {
            let r = t.getOptions()
              , {publicKey: i} = t.getDsn() || {}
              , {segment: o} = n && n.getUser() || {}
              , s = (0,
            O.Jr)({
                environment: r.environment || eg.J,
                release: r.release,
                user_segment: o,
                public_key: i,
                trace_id: e
            });
            return t.emit && t.emit("createDsc", s),
            s
        }
        var e_ = n(21170);
        let ey = new WeakMap
          , ev = "Not capturing exception because it's already been captured.";
        class eb {
            constructor(e) {
                if (this._options = e,
                this._integrations = {},
                this._integrationsInitialized = !1,
                this._numProcessing = 0,
                this._outcomes = {},
                this._hooks = {},
                e.dsn ? this._dsn = function(e) {
                    let t = "string" == typeof e ? ei(e) : eo(e);
                    if (t && function(e) {
                        if (!("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__))
                            return !0;
                        let {port: t, projectId: n, protocol: r} = e
                          , i = ["protocol", "publicKey", "host", "projectId"].find(t=>!e[t] && (E.kg.error(`Invalid Sentry Dsn: ${t} missing`),
                        !0));
                        return !i && (n.match(/^\d+$/) ? "http" === r || "https" === r ? !(t && isNaN(parseInt(t, 10))) || (E.kg.error(`Invalid Sentry Dsn: Invalid port ${t}`),
                        !1) : (E.kg.error(`Invalid Sentry Dsn: Invalid protocol ${r}`),
                        !1) : (E.kg.error(`Invalid Sentry Dsn: Invalid projectId ${n}`),
                        !1))
                    }(t))
                        return t
                }(e.dsn) : ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("No DSN provided, client will not do anything."),
                this._dsn) {
                    let t = function(e, t={}) {
                        let n = "string" == typeof t ? t : t.tunnel
                          , r = "string" != typeof t && t._metadata ? t._metadata.sdk : void 0;
                        return n || `${function(e) {
                            let t = e.protocol ? `${e.protocol}:` : ""
                              , n = e.port ? `:${e.port}` : "";
                            return `${t}//${e.host}${n}${e.path ? `/${e.path}` : ""}/api/`
                        }(e)}${e.projectId}/envelope/?${(0,
                        O._j)({
                            sentry_key: e.publicKey,
                            sentry_version: "7",
                            ...r && {
                                sentry_client: `${r.name}/${r.version}`
                            }
                        })}`
                    }(this._dsn, e);
                    this._transport = e.transport({
                        recordDroppedEvent: this.recordDroppedEvent.bind(this),
                        ...e.transportOptions,
                        url: t
                    })
                }
            }
            captureException(e, t, n) {
                if ((0,
                w.YO)(e)) {
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(ev);
                    return
                }
                let r = t && t.event_id;
                return this._process(this.eventFromException(e, t).then(e=>this._captureEvent(e, t, n)).then(e=>{
                    r = e
                }
                )),
                r
            }
            captureMessage(e, t, n, r) {
                let i = n && n.event_id
                  , o = (0,
                V.pt)(e) ? this.eventFromMessage(String(e), t, n) : this.eventFromException(e, n);
                return this._process(o.then(e=>this._captureEvent(e, n, r)).then(e=>{
                    i = e
                }
                )),
                i
            }
            captureEvent(e, t, n) {
                if (t && t.originalException && (0,
                w.YO)(t.originalException)) {
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(ev);
                    return
                }
                let r = t && t.event_id;
                return this._process(this._captureEvent(e, t, n).then(e=>{
                    r = e
                }
                )),
                r
            }
            captureSession(e) {
                if (!this._isEnabled()) {
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("SDK not enabled, will not capture session.");
                    return
                }
                "string" != typeof e.release ? ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("Discarded session because of missing or non-string release") : (this.sendSession(e),
                (0,
                ef.CT)(e, {
                    init: !1
                }))
            }
            getDsn() {
                return this._dsn
            }
            getOptions() {
                return this._options
            }
            getSdkMetadata() {
                return this._options._metadata
            }
            getTransport() {
                return this._transport
            }
            flush(e) {
                let t = this._transport;
                return t ? this._isClientDoneProcessing(e).then(n=>t.flush(e).then(e=>n && e)) : (0,
                es.WD)(!0)
            }
            close(e) {
                return this.flush(e).then(e=>(this.getOptions().enabled = !1,
                e))
            }
            setupIntegrations() {
                this._isEnabled() && !this._integrationsInitialized && (this._integrations = function(e) {
                    let t = {};
                    return e.forEach(e=>{
                        e && I(e, t)
                    }
                    ),
                    t
                }(this._options.integrations),
                this._integrationsInitialized = !0)
            }
            getIntegrationById(e) {
                return this._integrations[e]
            }
            getIntegration(e) {
                try {
                    return this._integrations[e.id] || null
                } catch (t) {
                    return ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`Cannot retrieve integration ${e.id} from the current Client`),
                    null
                }
            }
            addIntegration(e) {
                I(e, this._integrations)
            }
            sendEvent(e, t={}) {
                if (this._dsn) {
                    let n = function(e, t, n, r) {
                        var i, o;
                        let s = ep(n)
                          , a = e.type && "replay_event" !== e.type ? e.type : "event";
                        i = e,
                        (o = n && n.sdk) && (i.sdk = i.sdk || {},
                        i.sdk.name = i.sdk.name || o.name,
                        i.sdk.version = i.sdk.version || o.version,
                        i.sdk.integrations = [...i.sdk.integrations || [], ...o.integrations || []],
                        i.sdk.packages = [...i.sdk.packages || [], ...o.packages || []]);
                        let l = function(e, t, n, r) {
                            let i = e.sdkProcessingMetadata && e.sdkProcessingMetadata.dynamicSamplingContext;
                            return {
                                event_id: e.event_id,
                                sent_at: new Date().toISOString(),
                                ...t && {
                                    sdk: t
                                },
                                ...!!n && {
                                    dsn: er(r)
                                },
                                ...i && {
                                    trace: (0,
                                    O.Jr)({
                                        ...i
                                    })
                                }
                            }
                        }(e, s, r, t);
                        delete e.sdkProcessingMetadata;
                        let u = [{
                            type: a
                        }, e];
                        return el(l, [u])
                    }(e, this._dsn, this._options._metadata, this._options.tunnel);
                    for (let r of t.attachments || [])
                        n = function(e, t) {
                            let[n,r] = e;
                            return [n, [...r, t]]
                        }(n, function(e, t) {
                            let n = "string" == typeof e.data ? ec(e.data, t) : e.data;
                            return [(0,
                            O.Jr)({
                                type: "attachment",
                                length: n.length,
                                filename: e.filename,
                                content_type: e.contentType,
                                attachment_type: e.attachmentType
                            }), n]
                        }(r, this._options.transportOptions && this._options.transportOptions.textEncoder));
                    let i = this._sendEnvelope(n);
                    i && i.then(t=>this.emit("afterSendEvent", e, t), null)
                }
            }
            sendSession(e) {
                if (this._dsn) {
                    let t = function(e, t, n, r) {
                        let i = ep(n)
                          , o = {
                            sent_at: new Date().toISOString(),
                            ...i && {
                                sdk: i
                            },
                            ...!!r && {
                                dsn: er(t)
                            }
                        }
                          , s = "aggregates"in e ? [{
                            type: "sessions"
                        }, e] : [{
                            type: "session"
                        }, e.toJSON()];
                        return el(o, [s])
                    }(e, this._dsn, this._options._metadata, this._options.tunnel);
                    this._sendEnvelope(t)
                }
            }
            recordDroppedEvent(e, t, n) {
                if (this._options.sendClientReports) {
                    let r = `${e}:${t}`;
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`Adding outcome: "${r}"`),
                    this._outcomes[r] = this._outcomes[r] + 1 || 1
                }
            }
            on(e, t) {
                this._hooks[e] || (this._hooks[e] = []),
                this._hooks[e].push(t)
            }
            emit(e, ...t) {
                this._hooks[e] && this._hooks[e].forEach(e=>e(...t))
            }
            _updateSessionFromEvent(e, t) {
                let n = !1
                  , r = !1
                  , i = t.exception && t.exception.values;
                if (i)
                    for (let o of (r = !0,
                    i)) {
                        let s = o.mechanism;
                        if (s && !1 === s.handled) {
                            n = !0;
                            break
                        }
                    }
                let a = "ok" === e.status
                  , l = a && 0 === e.errors || a && n;
                l && ((0,
                ef.CT)(e, {
                    ...n && {
                        status: "crashed"
                    },
                    errors: e.errors || Number(r || n)
                }),
                this.captureSession(e))
            }
            _isClientDoneProcessing(e) {
                return new es.cW(t=>{
                    let n = 0
                      , r = setInterval(()=>{
                        0 == this._numProcessing ? (clearInterval(r),
                        t(!0)) : (n += 1,
                        e && n >= e && (clearInterval(r),
                        t(!1)))
                    }
                    , 1)
                }
                )
            }
            _isEnabled() {
                return !1 !== this.getOptions().enabled && void 0 !== this._dsn
            }
            _prepareEvent(e, t, n) {
                let r = this.getOptions()
                  , i = Object.keys(this._integrations);
                return !t.integrations && i.length > 0 && (t.integrations = i),
                (function(e, t, n, r) {
                    var i;
                    let {normalizeDepth: o=3, normalizeMaxBreadth: s=1e3} = e
                      , a = {
                        ...t,
                        event_id: t.event_id || n.event_id || (0,
                        w.DM)(),
                        timestamp: t.timestamp || (0,
                        e_.yW)()
                    }
                      , l = n.integrations || e.integrations.map(e=>e.name);
                    (function(e, t) {
                        let {environment: n, release: r, dist: i, maxValueLength: o=250} = t;
                        "environment"in e || (e.environment = "environment"in t ? n : eg.J),
                        void 0 === e.release && void 0 !== r && (e.release = r),
                        void 0 === e.dist && void 0 !== i && (e.dist = i),
                        e.message && (e.message = (0,
                        x.$G)(e.message, o));
                        let s = e.exception && e.exception.values && e.exception.values[0];
                        s && s.value && (s.value = (0,
                        x.$G)(s.value, o));
                        let a = e.request;
                        a && a.url && (a.url = (0,
                        x.$G)(a.url, o))
                    }
                    )(a, e),
                    i = a,
                    l.length > 0 && (i.sdk = i.sdk || {},
                    i.sdk.integrations = [...i.sdk.integrations || [], ...l]),
                    void 0 === t.type && function(e, t) {
                        let n;
                        let r = B.n2._sentryDebugIds;
                        if (!r)
                            return;
                        let i = ey.get(t);
                        i ? n = i : (n = new Map,
                        ey.set(t, n));
                        let o = Object.keys(r).reduce((e,i)=>{
                            let o;
                            let s = n.get(i);
                            s ? o = s : (o = t(i),
                            n.set(i, o));
                            for (let a = o.length - 1; a >= 0; a--) {
                                let l = o[a];
                                if (l.filename) {
                                    e[l.filename] = r[i];
                                    break
                                }
                            }
                            return e
                        }
                        , {});
                        try {
                            e.exception.values.forEach(e=>{
                                e.stacktrace.frames.forEach(e=>{
                                    e.filename && (e.debug_id = o[e.filename])
                                }
                                )
                            }
                            )
                        } catch (s) {}
                    }(a, e.stackParser);
                    let u = r;
                    n.captureContext && (u = C.s.clone(u).update(n.captureContext));
                    let c = (0,
                    es.WD)(a);
                    if (u) {
                        if (u.getAttachments) {
                            let d = [...n.attachments || [], ...u.getAttachments()];
                            d.length && (n.attachments = d)
                        }
                        c = u.applyToEvent(a, n)
                    }
                    return c.then(e=>(e && function(e) {
                        let t = {};
                        try {
                            e.exception.values.forEach(e=>{
                                e.stacktrace.frames.forEach(e=>{
                                    e.debug_id && (e.abs_path ? t[e.abs_path] = e.debug_id : e.filename && (t[e.filename] = e.debug_id),
                                    delete e.debug_id)
                                }
                                )
                            }
                            )
                        } catch (n) {}
                        if (0 === Object.keys(t).length)
                            return;
                        e.debug_meta = e.debug_meta || {},
                        e.debug_meta.images = e.debug_meta.images || [];
                        let r = e.debug_meta.images;
                        Object.keys(t).forEach(e=>{
                            r.push({
                                type: "sourcemap",
                                code_file: e,
                                debug_id: t[e]
                            })
                        }
                        )
                    }(e),
                    "number" == typeof o && o > 0) ? function(e, t, n) {
                        if (!e)
                            return null;
                        let r = {
                            ...e,
                            ...e.breadcrumbs && {
                                breadcrumbs: e.breadcrumbs.map(e=>({
                                    ...e,
                                    ...e.data && {
                                        data: ea(e.data, t, n)
                                    }
                                }))
                            },
                            ...e.user && {
                                user: ea(e.user, t, n)
                            },
                            ...e.contexts && {
                                contexts: ea(e.contexts, t, n)
                            },
                            ...e.extra && {
                                extra: ea(e.extra, t, n)
                            }
                        };
                        return e.contexts && e.contexts.trace && r.contexts && (r.contexts.trace = e.contexts.trace,
                        e.contexts.trace.data && (r.contexts.trace.data = ea(e.contexts.trace.data, t, n))),
                        e.spans && (r.spans = e.spans.map(e=>(e.data && (e.data = ea(e.data, t, n)),
                        e))),
                        r
                    }(e, o, s) : e)
                }
                )(r, e, t, n).then(e=>{
                    if (null === e)
                        return e;
                    let {propagationContext: t} = e.sdkProcessingMetadata || {}
                      , r = e.contexts && e.contexts.trace;
                    if (!r && t) {
                        let {traceId: i, spanId: o, parentSpanId: s, dsc: a} = t;
                        e.contexts = {
                            trace: {
                                trace_id: i,
                                span_id: o,
                                parent_span_id: s
                            },
                            ...e.contexts
                        };
                        let l = a || em(i, this, n);
                        e.sdkProcessingMetadata = {
                            dynamicSamplingContext: l,
                            ...e.sdkProcessingMetadata
                        }
                    }
                    return e
                }
                )
            }
            _captureEvent(e, t={}, n) {
                return this._processEvent(e, t, n).then(e=>e.event_id, e=>{
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && ("log" === e.logLevel ? E.kg.log(e.message) : E.kg.warn(e))
                }
                )
            }
            _processEvent(e, t, n) {
                let r = this.getOptions()
                  , {sampleRate: i} = r;
                if (!this._isEnabled())
                    return (0,
                    es.$2)(new eh("SDK not enabled, will not capture event.","log"));
                let o = eE(e)
                  , s = eS(e)
                  , a = e.type || "error"
                  , l = `before send for type \`${a}\``;
                if (s && "number" == typeof i && Math.random() > i)
                    return this.recordDroppedEvent("sample_rate", "error", e),
                    (0,
                    es.$2)(new eh(`Discarding event because it's not included in the random sample (sampling rate = ${i})`,"log"));
                let u = "replay_event" === a ? "replay" : a;
                return this._prepareEvent(e, t, n).then(n=>{
                    if (null === n)
                        throw this.recordDroppedEvent("event_processor", u, e),
                        new eh("An event processor returned `null`, will not send event.","log");
                    let i = t.data && !0 === t.data.__sentry__;
                    if (i)
                        return n;
                    let o = function(e, t, n) {
                        let {beforeSend: r, beforeSendTransaction: i} = e;
                        return eS(t) && r ? r(t, n) : eE(t) && i ? i(t, n) : t
                    }(r, n, t);
                    return function(e, t) {
                        let n = `${t} must return \`null\` or a valid event.`;
                        if ((0,
                        V.J8)(e))
                            return e.then(e=>{
                                if (!(0,
                                V.PO)(e) && null !== e)
                                    throw new eh(n);
                                return e
                            }
                            , e=>{
                                throw new eh(`${t} rejected with ${e}`)
                            }
                            );
                        if (!(0,
                        V.PO)(e) && null !== e)
                            throw new eh(n);
                        return e
                    }(o, l)
                }
                ).then(r=>{
                    if (null === r)
                        throw this.recordDroppedEvent("before_send", u, e),
                        new eh(`${l} returned \`null\`, will not send event.`,"log");
                    let i = n && n.getSession();
                    !o && i && this._updateSessionFromEvent(i, r);
                    let s = r.transaction_info;
                    return o && s && r.transaction !== e.transaction && (r.transaction_info = {
                        ...s,
                        source: "custom"
                    }),
                    this.sendEvent(r, t),
                    r
                }
                ).then(null, e=>{
                    if (e instanceof eh)
                        throw e;
                    throw this.captureException(e, {
                        data: {
                            __sentry__: !0
                        },
                        originalException: e
                    }),
                    new eh(`Event processing pipeline threw an error, original event will not be sent. Details have been sent as a new event.
Reason: ${e}`)
                }
                )
            }
            _process(e) {
                this._numProcessing++,
                e.then(e=>(this._numProcessing--,
                e), e=>(this._numProcessing--,
                e))
            }
            _sendEnvelope(e) {
                if (this._transport && this._dsn)
                    return this.emit("beforeEnvelope", e),
                    this._transport.send(e).then(null, e=>{
                        ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.error("Error while sending event:", e)
                    }
                    );
                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.error("Transport disabled")
            }
            _clearOutcomes() {
                let e = this._outcomes;
                return this._outcomes = {},
                Object.keys(e).map(t=>{
                    let[n,r] = t.split(":");
                    return {
                        reason: n,
                        category: r,
                        quantity: e[t]
                    }
                }
                )
            }
        }
        function eS(e) {
            return void 0 === e.type
        }
        function eE(e) {
            return "transaction" === e.type
        }
        var ew = n(68518);
        function ex(e, t) {
            let n = ek(e, t)
              , r = {
                type: t && t.name,
                value: function(e) {
                    let t = e && e.message;
                    return t ? t.error && "string" == typeof t.error.message ? t.error.message : t : "No error message"
                }(t)
            };
            return n.length && (r.stacktrace = {
                frames: n
            }),
            void 0 === r.type && "" === r.value && (r.value = "Unrecoverable error caught"),
            r
        }
        function eT(e, t) {
            return {
                exception: {
                    values: [ex(e, t)]
                }
            }
        }
        function ek(e, t) {
            let n = t.stacktrace || t.stack || ""
              , r = function(e) {
                if (e) {
                    if ("number" == typeof e.framesToPop)
                        return e.framesToPop;
                    if (eR.test(e.message))
                        return 1
                }
                return 0
            }(t);
            try {
                return e(n, r)
            } catch (i) {}
            return []
        }
        let eR = /Minified React error #\d+;/i;
        function eD(e, t, n, r, i) {
            let o;
            if ((0,
            V.VW)(t) && t.error)
                return eT(e, t.error);
            if ((0,
            V.TX)(t) || (0,
            V.fm)(t)) {
                if ("stack"in t)
                    o = eT(e, t);
                else {
                    let s = t.name || ((0,
                    V.TX)(t) ? "DOMError" : "DOMException")
                      , a = t.message ? `${s}: ${t.message}` : s;
                    o = eO(e, a, n, r),
                    (0,
                    w.Db)(o, a)
                }
                return "code"in t && (o.tags = {
                    ...o.tags,
                    "DOMException.code": `${t.code}`
                }),
                o
            }
            return (0,
            V.VZ)(t) ? eT(e, t) : (0,
            V.PO)(t) || (0,
            V.cO)(t) ? (o = function(e, t, n, r) {
                let i = (0,
                g.Gd)()
                  , o = i.getClient()
                  , s = o && o.getOptions().normalizeDepth
                  , a = {
                    exception: {
                        values: [{
                            type: (0,
                            V.cO)(t) ? t.constructor.name : r ? "UnhandledRejection" : "Error",
                            value: function(e, {isUnhandledRejection: t}) {
                                let n = (0,
                                O.zf)(e)
                                  , r = t ? "promise rejection" : "exception";
                                if ((0,
                                V.VW)(e))
                                    return `Event \`ErrorEvent\` captured as ${r} with message \`${e.message}\``;
                                if ((0,
                                V.cO)(e)) {
                                    let i = function(e) {
                                        try {
                                            let t = Object.getPrototypeOf(e);
                                            return t ? t.constructor.name : void 0
                                        } catch (n) {}
                                    }(e);
                                    return `Event \`${i}\` (type=${e.type}) captured as ${r}`
                                }
                                return `Object captured as ${r} with keys: ${n}`
                            }(t, {
                                isUnhandledRejection: r
                            })
                        }]
                    },
                    extra: {
                        __serialized__: function e(t, n=3, r=102400) {
                            let i = ea(t, n);
                            return ~-encodeURI(JSON.stringify(i)).split(/%..|./).length > r ? e(t, n - 1, r) : i
                        }(t, s)
                    }
                };
                if (n) {
                    let l = ek(e, n);
                    l.length && (a.exception.values[0].stacktrace = {
                        frames: l
                    })
                }
                return a
            }(e, t, n, i),
            (0,
            w.EG)(o, {
                synthetic: !0
            }),
            o) : (o = eO(e, t, n, r),
            (0,
            w.Db)(o, `${t}`, void 0),
            (0,
            w.EG)(o, {
                synthetic: !0
            }),
            o)
        }
        function eO(e, t, n, r) {
            let i = {
                message: t
            };
            if (r && n) {
                let o = ek(e, n);
                o.length && (i.exception = {
                    values: [{
                        value: t,
                        stacktrace: {
                            frames: o
                        }
                    }]
                })
            }
            return i
        }
        var eN = n(64487);
        let eC = B.n2
          , e$ = 0;
        function eI(e, t={}, n) {
            if ("function" != typeof e)
                return e;
            try {
                let r = e.__sentry_wrapped__;
                if (r)
                    return r;
                if ((0,
                O.HK)(e))
                    return e
            } catch (i) {
                return e
            }
            let o = function() {
                let r = Array.prototype.slice.call(arguments);
                try {
                    n && "function" == typeof n && n.apply(this, arguments);
                    let i = r.map(e=>eI(e, t));
                    return e.apply(this, i)
                } catch (o) {
                    throw e$++,
                    setTimeout(()=>{
                        e$--
                    }
                    ),
                    (0,
                    eN.$e)(e=>{
                        e.addEventProcessor(e=>(t.mechanism && ((0,
                        w.Db)(e, void 0, void 0),
                        (0,
                        w.EG)(e, t.mechanism)),
                        e.extra = {
                            ...e.extra,
                            arguments: r
                        },
                        e)),
                        (0,
                        eN.Tb)(o)
                    }
                    ),
                    o
                }
            };
            try {
                for (let s in e)
                    Object.prototype.hasOwnProperty.call(e, s) && (o[s] = e[s])
            } catch (a) {}
            (0,
            O.$Q)(o, e),
            (0,
            O.xp)(e, "__sentry_wrapped__", o);
            try {
                let l = Object.getOwnPropertyDescriptor(o, "name");
                l.configurable && Object.defineProperty(o, "name", {
                    get: ()=>e.name
                })
            } catch (u) {}
            return o
        }
        var eP = n(58464);
        let eA = ["fatal", "error", "warning", "log", "info", "debug"];
        function eL(e) {
            if (!e)
                return {};
            let t = e.match(/^(([^:/?#]+):)?(\/\/([^/?#]*))?([^?#]*)(\?([^#]*))?(#(.*))?$/);
            if (!t)
                return {};
            let n = t[6] || ""
              , r = t[8] || "";
            return {
                host: t[4],
                path: t[5],
                protocol: t[2],
                search: n,
                hash: r,
                relative: t[5] + n + r
            }
        }
        let eU = "Breadcrumbs";
        class ej {
            static __initStatic() {
                this.id = eU
            }
            constructor(e) {
                this.name = ej.id,
                this.options = {
                    console: !0,
                    dom: !0,
                    fetch: !0,
                    history: !0,
                    sentry: !0,
                    xhr: !0,
                    ...e
                }
            }
            setupOnce() {
                var e;
                this.options.console && J("console", eB),
                this.options.dom && J("dom", (e = this.options.dom,
                function(t) {
                    let n;
                    let r = "object" == typeof e ? e.serializeAttribute : void 0
                      , i = "object" == typeof e && "number" == typeof e.maxStringLength ? e.maxStringLength : void 0;
                    i && i > 1024 && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`\`dom.maxStringLength\` cannot exceed 1024, but a value of ${i} was configured. Sentry will use 1024 instead.`),
                    i = 1024),
                    "string" == typeof r && (r = [r]);
                    try {
                        let o = t.event;
                        n = o && o.target ? (0,
                        eP.Rt)(o.target, {
                            keyAttrs: r,
                            maxStringLength: i
                        }) : (0,
                        eP.Rt)(o, {
                            keyAttrs: r,
                            maxStringLength: i
                        })
                    } catch (s) {
                        n = "<unknown>"
                    }
                    0 !== n.length && (0,
                    g.Gd)().addBreadcrumb({
                        category: `ui.${t.name}`,
                        message: n
                    }, {
                        event: t.event,
                        name: t.name,
                        global: t.global
                    })
                }
                )),
                this.options.xhr && J("xhr", eY),
                this.options.fetch && J("fetch", eM),
                this.options.history && J("history", eG)
            }
            addSentryBreadcrumb(e) {
                this.options.sentry && (0,
                g.Gd)().addBreadcrumb({
                    category: `sentry.${"transaction" === e.type ? "transaction" : "event"}`,
                    event_id: e.event_id,
                    level: e.level,
                    message: (0,
                    w.jH)(e)
                }, {
                    event: e
                })
            }
        }
        function eB(e) {
            var t;
            for (let n = 0; n < e.args.length; n++)
                if ("ref=Ref<" === e.args[n]) {
                    e.args[n + 1] = "viewRef";
                    break
                }
            let r = {
                category: "console",
                data: {
                    arguments: e.args,
                    logger: "console"
                },
                level: "warn" === (t = e.level) ? "warning" : eA.includes(t) ? t : "log",
                message: (0,
                x.nK)(e.args, " ")
            };
            if ("assert" === e.level) {
                if (!1 !== e.args[0])
                    return;
                r.message = `Assertion failed: ${(0,
                x.nK)(e.args.slice(1), " ") || "console.assert"}`,
                r.data.arguments = e.args.slice(1)
            }
            (0,
            g.Gd)().addBreadcrumb(r, {
                input: e.args,
                level: e.level
            })
        }
        function eY(e) {
            let {startTimestamp: t, endTimestamp: n} = e
              , r = e.xhr[z];
            if (!t || !n || !r)
                return;
            let {method: i, url: o, status_code: s, body: a} = r
              , l = {
                xhr: e.xhr,
                input: a,
                startTimestamp: t,
                endTimestamp: n
            };
            (0,
            g.Gd)().addBreadcrumb({
                category: "xhr",
                data: {
                    method: i,
                    url: o,
                    status_code: s
                },
                type: "http"
            }, l)
        }
        function eM(e) {
            let {startTimestamp: t, endTimestamp: n} = e;
            if (!(!n || e.fetchData.url.match(/sentry_key/) && "POST" === e.fetchData.method)) {
                if (e.error) {
                    let r = e.fetchData
                      , i = {
                        data: e.error,
                        input: e.args,
                        startTimestamp: t,
                        endTimestamp: n
                    };
                    (0,
                    g.Gd)().addBreadcrumb({
                        category: "fetch",
                        data: r,
                        level: "error",
                        type: "http"
                    }, i)
                } else {
                    let o = {
                        ...e.fetchData,
                        status_code: e.response && e.response.status
                    }
                      , s = {
                        input: e.args,
                        response: e.response,
                        startTimestamp: t,
                        endTimestamp: n
                    };
                    (0,
                    g.Gd)().addBreadcrumb({
                        category: "fetch",
                        data: o,
                        type: "http"
                    }, s)
                }
            }
        }
        function eG(e) {
            let t = e.from
              , n = e.to
              , r = eL(eC.location.href)
              , i = eL(t)
              , o = eL(n);
            i.path || (i = r),
            r.protocol === o.protocol && r.host === o.host && (n = o.relative),
            r.protocol === i.protocol && r.host === i.host && (t = i.relative),
            (0,
            g.Gd)().addBreadcrumb({
                category: "navigation",
                data: {
                    from: t,
                    to: n
                }
            })
        }
        ej.__initStatic();
        class eV extends eb {
            constructor(e) {
                let t = eC.SENTRY_SDK_SOURCE || (0,
                ew.S)();
                e._metadata = e._metadata || {},
                e._metadata.sdk = e._metadata.sdk || {
                    name: "sentry.javascript.browser",
                    packages: [{
                        name: `${t}:@sentry/browser`,
                        version: S
                    }],
                    version: S
                },
                super(e),
                e.sendClientReports && eC.document && eC.document.addEventListener("visibilitychange", ()=>{
                    "hidden" === eC.document.visibilityState && this._flushOutcomes()
                }
                )
            }
            eventFromException(e, t) {
                return function(e, t, n, r) {
                    let i = n && n.syntheticException || void 0
                      , o = eD(e, t, i, r);
                    return (0,
                    w.EG)(o),
                    o.level = "error",
                    n && n.event_id && (o.event_id = n.event_id),
                    (0,
                    es.WD)(o)
                }(this._options.stackParser, e, t, this._options.attachStacktrace)
            }
            eventFromMessage(e, t="info", n) {
                return function(e, t, n="info", r, i) {
                    let o = r && r.syntheticException || void 0
                      , s = eO(e, t, o, i);
                    return s.level = n,
                    r && r.event_id && (s.event_id = r.event_id),
                    (0,
                    es.WD)(s)
                }(this._options.stackParser, e, t, n, this._options.attachStacktrace)
            }
            sendEvent(e, t) {
                let n = this.getIntegrationById(eU);
                n && n.addSentryBreadcrumb && n.addSentryBreadcrumb(e),
                super.sendEvent(e, t)
            }
            captureUserFeedback(e) {
                if (!this._isEnabled()) {
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("SDK not enabled, will not capture user feedback.");
                    return
                }
                let t = function(e, {metadata: t, tunnel: n, dsn: r}) {
                    let i = {
                        event_id: e.event_id,
                        sent_at: new Date().toISOString(),
                        ...t && t.sdk && {
                            sdk: {
                                name: t.sdk.name,
                                version: t.sdk.version
                            }
                        },
                        ...!!n && !!r && {
                            dsn: er(r)
                        }
                    };
                    return el(i, [[{
                        type: "user_report"
                    }, e]])
                }(e, {
                    metadata: this.getSdkMetadata(),
                    dsn: this.getDsn(),
                    tunnel: this.getOptions().tunnel
                });
                this._sendEnvelope(t)
            }
            _prepareEvent(e, t, n) {
                return e.platform = e.platform || "javascript",
                super._prepareEvent(e, t, n)
            }
            _flushOutcomes() {
                let e = this._clearOutcomes();
                if (0 === e.length) {
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("No outcomes to send");
                    return
                }
                if (!this._dsn) {
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("No dsn provided, will not send outcomes");
                    return
                }
                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("Sending outcomes:", e);
                let t = function(e, t, n) {
                    let r = [{
                        type: "client_report"
                    }, {
                        timestamp: (0,
                        e_.yW)(),
                        discarded_events: e
                    }];
                    return el(t ? {
                        dsn: t
                    } : {}, [r])
                }(e, this._options.tunnel && er(this._dsn));
                this._sendEnvelope(t)
            }
        }
        class eH {
            static __initStatic() {
                this.id = "GlobalHandlers"
            }
            constructor(e) {
                this.name = eH.id,
                this._options = {
                    onerror: !0,
                    onunhandledrejection: !0,
                    ...e
                },
                this._installFunc = {
                    onerror: eF,
                    onunhandledrejection: ez
                }
            }
            setupOnce() {
                Error.stackTraceLimit = 50;
                let e = this._options;
                for (let t in e) {
                    var n;
                    let r = this._installFunc[t];
                    r && e[t] && (n = t,
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`Global Handler attached: ${n}`),
                    r(),
                    this._installFunc[t] = void 0)
                }
            }
        }
        function eF() {
            J("error", e=>{
                let[t,n,r] = eJ();
                if (!t.getIntegration(eH))
                    return;
                let {msg: i, url: o, line: s, column: a, error: l} = e;
                if (e$ > 0 || l && l.__sentry_own_request__)
                    return;
                let u = void 0 === l && (0,
                V.HD)(i) ? function(e, t, n, r) {
                    let i = (0,
                    V.VW)(e) ? e.message : e
                      , o = "Error"
                      , s = i.match(/^(?:[Uu]ncaught (?:exception: )?)?(?:((?:Eval|Internal|Range|Reference|Syntax|Type|URI|)Error): )?(.*)$/i);
                    s && (o = s[1],
                    i = s[2]);
                    let a = {
                        exception: {
                            values: [{
                                type: o,
                                value: i
                            }]
                        }
                    };
                    return eq(a, t, n, r)
                }(i, o, s, a) : eq(eD(n, l || i, void 0, r, !1), o, s, a);
                u.level = "error",
                eW(t, l, u, "onerror")
            }
            )
        }
        function ez() {
            J("unhandledrejection", e=>{
                let[t,n,r] = eJ();
                if (!t.getIntegration(eH))
                    return;
                let i = e;
                try {
                    "reason"in e ? i = e.reason : "detail"in e && "reason"in e.detail && (i = e.detail.reason)
                } catch (o) {}
                if (e$ > 0 || i && i.__sentry_own_request__)
                    return !0;
                let s = (0,
                V.pt)(i) ? {
                    exception: {
                        values: [{
                            type: "UnhandledRejection",
                            value: `Non-Error promise rejection captured with value: ${String(i)}`
                        }]
                    }
                } : eD(n, i, void 0, r, !0);
                s.level = "error",
                eW(t, i, s, "onunhandledrejection")
            }
            )
        }
        function eq(e, t, n, r) {
            let i = e.exception = e.exception || {}
              , o = i.values = i.values || []
              , s = o[0] = o[0] || {}
              , a = s.stacktrace = s.stacktrace || {}
              , l = a.frames = a.frames || []
              , u = isNaN(parseInt(r, 10)) ? void 0 : r
              , c = isNaN(parseInt(n, 10)) ? void 0 : n
              , d = (0,
            V.HD)(t) && t.length > 0 ? t : (0,
            eP.l4)();
            return 0 === l.length && l.push({
                colno: u,
                filename: d,
                function: "?",
                in_app: !0,
                lineno: c
            }),
            e
        }
        function eW(e, t, n, r) {
            (0,
            w.EG)(n, {
                handled: !1,
                type: r
            }),
            e.captureEvent(n, {
                originalException: t
            })
        }
        function eJ() {
            let e = (0,
            g.Gd)()
              , t = e.getClient()
              , n = t && t.getOptions() || {
                stackParser: ()=>[],
                attachStacktrace: !1
            };
            return [e, n.stackParser, n.attachStacktrace]
        }
        eH.__initStatic();
        let eK = ["EventTarget", "Window", "Node", "ApplicationCache", "AudioTrackList", "ChannelMergerNode", "CryptoOperation", "EventSource", "FileReader", "HTMLUnknownElement", "IDBDatabase", "IDBRequest", "IDBTransaction", "KeyOperation", "MediaController", "MessagePort", "ModalWindow", "Notification", "SVGElementInstance", "Screen", "TextTrack", "TextTrackCue", "TextTrackList", "WebSocket", "WebSocketWorker", "Worker", "XMLHttpRequest", "XMLHttpRequestEventTarget", "XMLHttpRequestUpload"];
        class eX {
            static __initStatic() {
                this.id = "TryCatch"
            }
            constructor(e) {
                this.name = eX.id,
                this._options = {
                    XMLHttpRequest: !0,
                    eventTarget: !0,
                    requestAnimationFrame: !0,
                    setInterval: !0,
                    setTimeout: !0,
                    ...e
                }
            }
            setupOnce() {
                this._options.setTimeout && (0,
                O.hl)(eC, "setTimeout", eZ),
                this._options.setInterval && (0,
                O.hl)(eC, "setInterval", eZ),
                this._options.requestAnimationFrame && (0,
                O.hl)(eC, "requestAnimationFrame", eQ),
                this._options.XMLHttpRequest && "XMLHttpRequest"in eC && (0,
                O.hl)(XMLHttpRequest.prototype, "send", e0);
                let e = this._options.eventTarget;
                if (e) {
                    let t = Array.isArray(e) ? e : eK;
                    t.forEach(e1)
                }
            }
        }
        function eZ(e) {
            return function(...t) {
                let n = t[0];
                return t[0] = eI(n, {
                    mechanism: {
                        data: {
                            function: j(e)
                        },
                        handled: !0,
                        type: "instrument"
                    }
                }),
                e.apply(this, t)
            }
        }
        function eQ(e) {
            return function(t) {
                return e.apply(this, [eI(t, {
                    mechanism: {
                        data: {
                            function: "requestAnimationFrame",
                            handler: j(e)
                        },
                        handled: !0,
                        type: "instrument"
                    }
                })])
            }
        }
        function e0(e) {
            return function(...t) {
                let n = this;
                return ["onload", "onerror", "onprogress", "onreadystatechange"].forEach(e=>{
                    e in n && "function" == typeof n[e] && (0,
                    O.hl)(n, e, function(t) {
                        let n = {
                            mechanism: {
                                data: {
                                    function: e,
                                    handler: j(t)
                                },
                                handled: !0,
                                type: "instrument"
                            }
                        }
                          , r = (0,
                        O.HK)(t);
                        return r && (n.mechanism.data.handler = j(r)),
                        eI(t, n)
                    })
                }
                ),
                e.apply(this, t)
            }
        }
        function e1(e) {
            let t = eC[e] && eC[e].prototype;
            t && t.hasOwnProperty && t.hasOwnProperty("addEventListener") && ((0,
            O.hl)(t, "addEventListener", function(t) {
                return function(n, r, i) {
                    try {
                        "function" == typeof r.handleEvent && (r.handleEvent = eI(r.handleEvent, {
                            mechanism: {
                                data: {
                                    function: "handleEvent",
                                    handler: j(r),
                                    target: e
                                },
                                handled: !0,
                                type: "instrument"
                            }
                        }))
                    } catch (o) {}
                    return t.apply(this, [n, eI(r, {
                        mechanism: {
                            data: {
                                function: "addEventListener",
                                handler: j(r),
                                target: e
                            },
                            handled: !0,
                            type: "instrument"
                        }
                    }), i])
                }
            }),
            (0,
            O.hl)(t, "removeEventListener", function(e) {
                return function(t, n, r) {
                    try {
                        let i = n && n.__sentry_wrapped__;
                        i && e.call(this, t, i, r)
                    } catch (o) {}
                    return e.call(this, t, n, r)
                }
            }))
        }
        function e2(e, t) {
            e.mechanism = e.mechanism || {
                type: "generic",
                handled: !0
            },
            e.mechanism = {
                ...e.mechanism,
                is_exception_group: !0,
                exception_id: t
            }
        }
        function e3(e, t, n, r) {
            e.mechanism = e.mechanism || {
                type: "generic",
                handled: !0
            },
            e.mechanism = {
                ...e.mechanism,
                type: "chained",
                source: t,
                exception_id: n,
                parent_id: r
            }
        }
        eX.__initStatic();
        class e4 {
            static __initStatic() {
                this.id = "LinkedErrors"
            }
            constructor(e={}) {
                this.name = e4.id,
                this._key = e.key || "cause",
                this._limit = e.limit || 5
            }
            setupOnce(e, t) {
                e((e,n)=>{
                    let r = t()
                      , i = r.getClient()
                      , o = r.getIntegration(e4);
                    if (!i || !o)
                        return e;
                    let s = i.getOptions();
                    return !function(e, t, n=250, r, i, o, s) {
                        if (!o.exception || !o.exception.values || !s || !(0,
                        V.V9)(s.originalException, Error))
                            return;
                        let a = o.exception.values.length > 0 ? o.exception.values[o.exception.values.length - 1] : void 0;
                        a && (o.exception.values = (function e(t, n, r, i, o, s, a, l) {
                            if (s.length >= r + 1)
                                return s;
                            let u = [...s];
                            if ((0,
                            V.V9)(i[o], Error)) {
                                e2(a, l);
                                let c = t(n, i[o])
                                  , d = u.length;
                                e3(c, o, d, l),
                                u = e(t, n, r, i[o], o, [c, ...u], c, d)
                            }
                            return Array.isArray(i.errors) && i.errors.forEach((i,s)=>{
                                if ((0,
                                V.V9)(i, Error)) {
                                    e2(a, l);
                                    let c = t(n, i)
                                      , d = u.length;
                                    e3(c, `errors[${s}]`, d, l),
                                    u = e(t, n, r, i, o, [c, ...u], c, d)
                                }
                            }
                            ),
                            u
                        }
                        )(e, t, i, s.originalException, r, o.exception.values, a, 0).map(e=>(e.value && (e.value = (0,
                        x.$G)(e.value, n)),
                        e)))
                    }(ex, s.stackParser, s.maxValueLength, o._key, o._limit, e, n),
                    e
                }
                )
            }
        }
        e4.__initStatic();
        class e5 {
            static __initStatic() {
                this.id = "HttpContext"
            }
            constructor() {
                this.name = e5.id
            }
            setupOnce() {
                (0,
                C.c)(e=>{
                    if ((0,
                    g.Gd)().getIntegration(e5)) {
                        if (!eC.navigator && !eC.location && !eC.document)
                            return e;
                        let t = e.request && e.request.url || eC.location && eC.location.href
                          , {referrer: n} = eC.document || {}
                          , {userAgent: r} = eC.navigator || {}
                          , i = {
                            ...e.request && e.request.headers,
                            ...n && {
                                Referer: n
                            },
                            ...r && {
                                "User-Agent": r
                            }
                        }
                          , o = {
                            ...e.request,
                            ...t && {
                                url: t
                            },
                            headers: i
                        };
                        return {
                            ...e,
                            request: o
                        }
                    }
                    return e
                }
                )
            }
        }
        e5.__initStatic();
        class e6 {
            static __initStatic() {
                this.id = "Dedupe"
            }
            constructor() {
                this.name = e6.id
            }
            setupOnce(e, t) {
                let n = e=>{
                    if (e.type)
                        return e;
                    let n = t().getIntegration(e6);
                    if (n) {
                        try {
                            var r;
                            if ((r = n._previousEvent) && (function(e, t) {
                                let n = e.message
                                  , r = t.message;
                                return !!((n || r) && (!n || r) && (n || !r) && n === r && e9(e, t) && e8(e, t))
                            }(e, r) || function(e, t) {
                                let n = e7(t)
                                  , r = e7(e);
                                return !!(n && r && n.type === r.type && n.value === r.value && e9(e, t) && e8(e, t))
                            }(e, r)))
                                return ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("Event dropped due to being a duplicate of previously captured event."),
                                null
                        } catch (i) {}
                        return n._previousEvent = e
                    }
                    return e
                }
                ;
                n.id = this.name,
                e(n)
            }
        }
        function e8(e, t) {
            let n = te(e)
              , r = te(t);
            if (!n && !r)
                return !0;
            if (n && !r || !n && r || r.length !== n.length)
                return !1;
            for (let i = 0; i < r.length; i++) {
                let o = r[i]
                  , s = n[i];
                if (o.filename !== s.filename || o.lineno !== s.lineno || o.colno !== s.colno || o.function !== s.function)
                    return !1
            }
            return !0
        }
        function e9(e, t) {
            let n = e.fingerprint
              , r = t.fingerprint;
            if (!n && !r)
                return !0;
            if (n && !r || !n && r)
                return !1;
            try {
                return !(n.join("") !== r.join(""))
            } catch (i) {
                return !1
            }
        }
        function e7(e) {
            return e.exception && e.exception.values && e.exception.values[0]
        }
        function te(e) {
            let t = e.exception;
            if (t)
                try {
                    return t.values[0].stacktrace.frames
                } catch (n) {}
        }
        function tt(e, t, n, r) {
            let i = {
                filename: e,
                function: t,
                in_app: !0
            };
            return void 0 !== n && (i.lineno = n),
            void 0 !== r && (i.colno = r),
            i
        }
        e6.__initStatic();
        let tn = /^\s*at (?:(.+?\)(?: \[.+\])?|.*?) ?\((?:address at )?)?(?:async )?((?:<anonymous>|[-a-z]+:|.*bundle|\/)?.*?)(?::(\d+))?(?::(\d+))?\)?\s*$/i
          , tr = /\((\S*)(?::(\d+))(?::(\d+))\)/
          , ti = e=>{
            let t = tn.exec(e);
            if (t) {
                let n = t[2] && 0 === t[2].indexOf("eval");
                if (n) {
                    let r = tr.exec(t[2]);
                    r && (t[2] = r[1],
                    t[3] = r[2],
                    t[4] = r[3])
                }
                let[i,o] = td(t[1] || "?", t[2]);
                return tt(o, i, t[3] ? +t[3] : void 0, t[4] ? +t[4] : void 0)
            }
        }
          , to = /^\s*(.*?)(?:\((.*?)\))?(?:^|@)?((?:[-a-z]+)?:\/.*?|\[native code\]|[^@]*(?:bundle|\d+\.js)|\/[\w\-. /=]+)(?::(\d+))?(?::(\d+))?\s*$/i
          , ts = /(\S+) line (\d+)(?: > eval line \d+)* > eval/i
          , ta = e=>{
            let t = to.exec(e);
            if (t) {
                let n = t[3] && t[3].indexOf(" > eval") > -1;
                if (n) {
                    let r = ts.exec(t[3]);
                    r && (t[1] = t[1] || "eval",
                    t[3] = r[1],
                    t[4] = r[2],
                    t[5] = "")
                }
                let i = t[3]
                  , o = t[1] || "?";
                return [o,i] = td(o, i),
                tt(i, o, t[4] ? +t[4] : void 0, t[5] ? +t[5] : void 0)
            }
        }
          , tl = /^\s*at (?:((?:\[object object\])?.+) )?\(?((?:[-a-z]+):.*?):(\d+)(?::(\d+))?\)?\s*$/i
          , tu = e=>{
            let t = tl.exec(e);
            return t ? tt(t[2], t[1] || "?", +t[3], t[4] ? +t[4] : void 0) : void 0
        }
          , tc = L(...[[30, ti], [50, ta], [40, tu]])
          , td = (e,t)=>{
            let n = -1 !== e.indexOf("safari-extension")
              , r = -1 !== e.indexOf("safari-web-extension");
            return n || r ? [-1 !== e.indexOf("@") ? e.split("@")[0] : "?", n ? `safari-extension:${t}` : `safari-web-extension:${t}`] : [e, t]
        }
        ;
        function tp(e, t, n=function(e) {
            let t = [];
            function n(e) {
                return t.splice(t.indexOf(e), 1)[0]
            }
            return {
                $: t,
                add: function(r) {
                    if (!(void 0 === e || t.length < e))
                        return (0,
                        es.$2)(new eh("Not adding Promise because buffer limit was reached."));
                    let i = r();
                    return -1 === t.indexOf(i) && t.push(i),
                    i.then(()=>n(i)).then(null, ()=>n(i).then(null, ()=>{}
                    )),
                    i
                },
                drain: function(e) {
                    return new es.cW((n,r)=>{
                        let i = t.length;
                        if (!i)
                            return n(!0);
                        let o = setTimeout(()=>{
                            e && e > 0 && n(!1)
                        }
                        , e);
                        t.forEach(e=>{
                            (0,
                            es.WD)(e).then(()=>{
                                --i || (clearTimeout(o),
                                n(!0))
                            }
                            , r)
                        }
                        )
                    }
                    )
                }
            }
        }(e.bufferSize || 30)) {
            let r = {}
              , i = e=>n.drain(e);
            function o(i) {
                let o = [];
                if (eu(i, (t,n)=>{
                    let i = ed[n];
                    if (function(e, t, n=Date.now()) {
                        return (e[t] || e.all || 0) > n
                    }(r, i)) {
                        let s = th(t, n);
                        e.recordDroppedEvent("ratelimit_backoff", i, s)
                    } else
                        o.push(t)
                }
                ),
                0 === o.length)
                    return (0,
                    es.WD)();
                let s = el(i[0], o)
                  , a = t=>{
                    eu(s, (n,r)=>{
                        let i = th(n, r);
                        e.recordDroppedEvent(t, ed[r], i)
                    }
                    )
                }
                  , l = ()=>t({
                    body: function(e, t) {
                        let[n,r] = e
                          , i = JSON.stringify(n);
                        function o(e) {
                            "string" == typeof i ? i = "string" == typeof e ? i + e : [ec(i, t), e] : i.push("string" == typeof e ? ec(e, t) : e)
                        }
                        for (let s of r) {
                            let[a,l] = s;
                            if (o(`
${JSON.stringify(a)}
`),
                            "string" == typeof l || l instanceof Uint8Array)
                                o(l);
                            else {
                                let u;
                                try {
                                    u = JSON.stringify(l)
                                } catch (c) {
                                    u = JSON.stringify(ea(l))
                                }
                                o(u)
                            }
                        }
                        return "string" == typeof i ? i : function(e) {
                            let t = e.reduce((e,t)=>e + t.length, 0)
                              , n = new Uint8Array(t)
                              , r = 0;
                            for (let i of e)
                                n.set(i, r),
                                r += i.length;
                            return n
                        }(i)
                    }(s, e.textEncoder)
                }).then(e=>(void 0 !== e.statusCode && (e.statusCode < 200 || e.statusCode >= 300) && ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`Sentry responded with status code ${e.statusCode} to sent event.`),
                r = function(e, {statusCode: t, headers: n}, r=Date.now()) {
                    let i = {
                        ...e
                    }
                      , o = n && n["x-sentry-rate-limits"]
                      , s = n && n["retry-after"];
                    if (o)
                        for (let a of o.trim().split(",")) {
                            let[l,u] = a.split(":", 2)
                              , c = parseInt(l, 10)
                              , d = (isNaN(c) ? 60 : c) * 1e3;
                            if (u)
                                for (let p of u.split(";"))
                                    i[p] = r + d;
                            else
                                i.all = r + d
                        }
                    else
                        s ? i.all = r + function(e, t=Date.now()) {
                            let n = parseInt(`${e}`, 10);
                            if (!isNaN(n))
                                return 1e3 * n;
                            let r = Date.parse(`${e}`);
                            return isNaN(r) ? 6e4 : r - t
                        }(s, r) : 429 === t && (i.all = r + 6e4);
                    return i
                }(r, e),
                e), e=>{
                    throw a("network_error"),
                    e
                }
                );
                return n.add(l).then(e=>e, e=>{
                    if (e instanceof eh)
                        return ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.error("Skipped sending event because buffer is full."),
                        a("queue_overflow"),
                        (0,
                        es.WD)();
                    throw e
                }
                )
            }
            return o.__sentry__baseTransport__ = !0,
            {
                send: o,
                flush: i
            }
        }
        function th(e, t) {
            if ("event" === t || "transaction" === t)
                return Array.isArray(e) ? e[1] : void 0
        }
        function tf(e, t=function() {
            if (u)
                return u;
            if (G(eC.fetch))
                return u = eC.fetch.bind(eC);
            let e = eC.document
              , t = eC.fetch;
            if (e && "function" == typeof e.createElement)
                try {
                    let n = e.createElement("iframe");
                    n.hidden = !0,
                    e.head.appendChild(n);
                    let r = n.contentWindow;
                    r && r.fetch && (t = r.fetch),
                    e.head.removeChild(n)
                } catch (i) {
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("Could not create sandbox iframe for pure fetch check, bailing to window.fetch: ", i)
                }
            return u = t.bind(eC)
        }()) {
            let n = 0
              , r = 0;
            return tp(e, function(i) {
                let o = i.body.length;
                n += o,
                r++;
                let s = {
                    body: i.body,
                    method: "POST",
                    referrerPolicy: "origin",
                    headers: e.headers,
                    keepalive: n <= 6e4 && r < 15,
                    ...e.fetchOptions
                };
                try {
                    return t(e.url, s).then(e=>(n -= o,
                    r--,
                    {
                        statusCode: e.status,
                        headers: {
                            "x-sentry-rate-limits": e.headers.get("X-Sentry-Rate-Limits"),
                            "retry-after": e.headers.get("Retry-After")
                        }
                    }))
                } catch (a) {
                    return u = void 0,
                    n -= o,
                    r--,
                    (0,
                    es.$2)(a)
                }
            })
        }
        function tg(e) {
            return tp(e, function(t) {
                return new es.cW((n,r)=>{
                    let i = new XMLHttpRequest;
                    for (let o in i.onerror = r,
                    i.onreadystatechange = ()=>{
                        4 === i.readyState && n({
                            statusCode: i.status,
                            headers: {
                                "x-sentry-rate-limits": i.getResponseHeader("X-Sentry-Rate-Limits"),
                                "retry-after": i.getResponseHeader("Retry-After")
                            }
                        })
                    }
                    ,
                    i.open("POST", e.url),
                    e.headers)
                        Object.prototype.hasOwnProperty.call(e.headers, o) && i.setRequestHeader(o, e.headers[o]);
                    i.send(t.body)
                }
                )
            })
        }
        let tm = [new R, new N, new eX, new ej, new eH, new e4, new e6, new e5];
        function t_(e) {
            e.startSession({
                ignoreDuration: !0
            }),
            e.captureSession()
        }
        let ty = "baggage"
          , tv = "sentry-"
          , tb = /^sentry-/;
        function tS(e) {
            if (!e)
                return;
            let t = Object.entries(e).reduce((e,[t,n])=>(n && (e[`${tv}${t}`] = n),
            e), {});
            return function(e) {
                if (0 !== Object.keys(e).length)
                    return Object.entries(e).reduce((e,[t,n],r)=>{
                        let i = `${encodeURIComponent(t)}=${encodeURIComponent(n)}`
                          , o = 0 === r ? i : `${e},${i}`;
                        return o.length > 8192 ? (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`Not adding key: ${t} with val: ${n} to baggage header due to exceeding baggage size limits.`),
                        e) : o
                    }
                    , "")
            }(t)
        }
        function tE(e) {
            return e.split(",").map(e=>e.split("=").map(e=>decodeURIComponent(e.trim()))).reduce((e,[t,n])=>(e[t] = n,
            e), {})
        }
        let tw = RegExp("^[ \\t]*([0-9a-f]{32})?-?([0-9a-f]{16})?-?([01])?[ \\t]*$");
        function tx(e, t) {
            let n = function(e) {
                let t;
                if (!e)
                    return;
                let n = e.match(tw);
                if (n)
                    return "1" === n[3] ? t = !0 : "0" === n[3] && (t = !1),
                    {
                        traceId: n[1],
                        parentSampled: t,
                        parentSpanId: n[2]
                    }
            }(e)
              , r = function(e) {
                if (!(0,
                V.HD)(e) && !Array.isArray(e))
                    return;
                let t = {};
                if (Array.isArray(e))
                    t = e.reduce((e,t)=>{
                        let n = tE(t);
                        return {
                            ...e,
                            ...n
                        }
                    }
                    , {});
                else {
                    if (!e)
                        return;
                    t = tE(e)
                }
                let n = Object.entries(t).reduce((e,[t,n])=>{
                    if (t.match(tb)) {
                        let r = t.slice(tv.length);
                        e[r] = n
                    }
                    return e
                }
                , {});
                return Object.keys(n).length > 0 ? n : void 0
            }(t)
              , {traceId: i, parentSpanId: o, parentSampled: s} = n || {}
              , a = {
                traceId: i || (0,
                w.DM)(),
                spanId: (0,
                w.DM)().substring(16),
                sampled: void 0 !== s && s
            };
            return o && (a.parentSpanId = o),
            r && (a.dsc = r),
            {
                traceparentData: n,
                dynamicSamplingContext: r,
                propagationContext: a
            }
        }
        function tT(e=(0,
        w.DM)(), t=(0,
        w.DM)().substring(16), n) {
            let r = "";
            return void 0 !== n && (r = n ? "-1" : "-0"),
            `${e}-${t}${r}`
        }
        class tk {
            constructor(e=1e3) {
                this._maxlen = e,
                this.spans = []
            }
            add(e) {
                this.spans.length > this._maxlen ? e.spanRecorder = void 0 : this.spans.push(e)
            }
        }
        class tR {
            constructor(e) {
                if (this.traceId = (0,
                w.DM)(),
                this.spanId = (0,
                w.DM)().substring(16),
                this.startTimestamp = (0,
                e_.ph)(),
                this.tags = {},
                this.data = {},
                this.instrumenter = "sentry",
                !e)
                    return this;
                e.traceId && (this.traceId = e.traceId),
                e.spanId && (this.spanId = e.spanId),
                e.parentSpanId && (this.parentSpanId = e.parentSpanId),
                "sampled"in e && (this.sampled = e.sampled),
                e.op && (this.op = e.op),
                e.description && (this.description = e.description),
                e.name && (this.description = e.name),
                e.data && (this.data = e.data),
                e.tags && (this.tags = e.tags),
                e.status && (this.status = e.status),
                e.startTimestamp && (this.startTimestamp = e.startTimestamp),
                e.endTimestamp && (this.endTimestamp = e.endTimestamp),
                e.instrumenter && (this.instrumenter = e.instrumenter)
            }
            startChild(e) {
                let t = new tR({
                    ...e,
                    parentSpanId: this.spanId,
                    sampled: this.sampled,
                    traceId: this.traceId
                });
                if (t.spanRecorder = this.spanRecorder,
                t.spanRecorder && t.spanRecorder.add(t),
                t.transaction = this.transaction,
                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && t.transaction) {
                    let n = e && e.op || "< unknown op >"
                      , r = t.transaction.name || "< unknown name >"
                      , i = t.transaction.spanId
                      , o = `[Tracing] Starting '${n}' span on transaction '${r}' (${i}).`;
                    t.transaction.metadata.spanMetadata[t.spanId] = {
                        logMessage: o
                    },
                    E.kg.log(o)
                }
                return t
            }
            setTag(e, t) {
                return this.tags = {
                    ...this.tags,
                    [e]: t
                },
                this
            }
            setData(e, t) {
                return this.data = {
                    ...this.data,
                    [e]: t
                },
                this
            }
            setStatus(e) {
                return this.status = e,
                this
            }
            setHttpStatus(e) {
                this.setTag("http.status_code", String(e)),
                this.setData("http.response.status_code", e);
                let t = function(e) {
                    if (e < 400 && e >= 100)
                        return "ok";
                    if (e >= 400 && e < 500)
                        switch (e) {
                        case 401:
                            return "unauthenticated";
                        case 403:
                            return "permission_denied";
                        case 404:
                            return "not_found";
                        case 409:
                            return "already_exists";
                        case 413:
                            return "failed_precondition";
                        case 429:
                            return "resource_exhausted";
                        default:
                            return "invalid_argument"
                        }
                    if (e >= 500 && e < 600)
                        switch (e) {
                        case 501:
                            return "unimplemented";
                        case 503:
                            return "unavailable";
                        case 504:
                            return "deadline_exceeded";
                        default:
                            return "internal_error"
                        }
                    return "unknown_error"
                }(e);
                return "unknown_error" !== t && this.setStatus(t),
                this
            }
            setName(e) {
                this.description = e
            }
            isSuccess() {
                return "ok" === this.status
            }
            finish(e) {
                if (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && this.transaction && this.transaction.spanId !== this.spanId) {
                    let {logMessage: t} = this.transaction.metadata.spanMetadata[this.spanId];
                    t && E.kg.log(t.replace("Starting", "Finishing"))
                }
                this.endTimestamp = "number" == typeof e ? e : (0,
                e_.ph)()
            }
            toTraceparent() {
                return tT(this.traceId, this.spanId, this.sampled)
            }
            toContext() {
                return (0,
                O.Jr)({
                    data: this.data,
                    description: this.description,
                    endTimestamp: this.endTimestamp,
                    op: this.op,
                    parentSpanId: this.parentSpanId,
                    sampled: this.sampled,
                    spanId: this.spanId,
                    startTimestamp: this.startTimestamp,
                    status: this.status,
                    tags: this.tags,
                    traceId: this.traceId
                })
            }
            updateWithContext(e) {
                return this.data = e.data || {},
                this.description = e.description,
                this.endTimestamp = e.endTimestamp,
                this.op = e.op,
                this.parentSpanId = e.parentSpanId,
                this.sampled = e.sampled,
                this.spanId = e.spanId || this.spanId,
                this.startTimestamp = e.startTimestamp || this.startTimestamp,
                this.status = e.status,
                this.tags = e.tags || {},
                this.traceId = e.traceId || this.traceId,
                this
            }
            getTraceContext() {
                return (0,
                O.Jr)({
                    data: Object.keys(this.data).length > 0 ? this.data : void 0,
                    description: this.description,
                    op: this.op,
                    parent_span_id: this.parentSpanId,
                    span_id: this.spanId,
                    status: this.status,
                    tags: Object.keys(this.tags).length > 0 ? this.tags : void 0,
                    trace_id: this.traceId
                })
            }
            toJSON() {
                return (0,
                O.Jr)({
                    data: Object.keys(this.data).length > 0 ? this.data : void 0,
                    description: this.description,
                    op: this.op,
                    parent_span_id: this.parentSpanId,
                    span_id: this.spanId,
                    start_timestamp: this.startTimestamp,
                    status: this.status,
                    tags: Object.keys(this.tags).length > 0 ? this.tags : void 0,
                    timestamp: this.endTimestamp,
                    trace_id: this.traceId
                })
            }
        }
        class tD extends tR {
            constructor(e, t) {
                super(e),
                delete this.description,
                this._measurements = {},
                this._contexts = {},
                this._hub = t || (0,
                g.Gd)(),
                this._name = e.name || "",
                this.metadata = {
                    source: "custom",
                    ...e.metadata,
                    spanMetadata: {}
                },
                this._trimEnd = e.trimEnd,
                this.transaction = this;
                let n = this.metadata.dynamicSamplingContext;
                n && (this._frozenDynamicSamplingContext = {
                    ...n
                })
            }
            get name() {
                return this._name
            }
            set name(e) {
                this.setName(e)
            }
            setName(e, t="custom") {
                this._name = e,
                this.metadata.source = t
            }
            initSpanRecorder(e=1e3) {
                this.spanRecorder || (this.spanRecorder = new tk(e)),
                this.spanRecorder.add(this)
            }
            setContext(e, t) {
                null === t ? delete this._contexts[e] : this._contexts[e] = t
            }
            setMeasurement(e, t, n="") {
                this._measurements[e] = {
                    value: t,
                    unit: n
                }
            }
            setMetadata(e) {
                this.metadata = {
                    ...this.metadata,
                    ...e
                }
            }
            finish(e) {
                if (void 0 !== this.endTimestamp)
                    return;
                this.name || (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("Transaction has no name, falling back to `<unlabeled transaction>`."),
                this.name = "<unlabeled transaction>"),
                super.finish(e);
                let t = this._hub.getClient();
                if (t && t.emit && t.emit("finishTransaction", this),
                !0 !== this.sampled) {
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Tracing] Discarding transaction because its trace was not chosen to be sampled."),
                    t && t.recordDroppedEvent("sample_rate", "transaction");
                    return
                }
                let n = this.spanRecorder ? this.spanRecorder.spans.filter(e=>e !== this && e.endTimestamp) : [];
                this._trimEnd && n.length > 0 && (this.endTimestamp = n.reduce((e,t)=>e.endTimestamp && t.endTimestamp ? e.endTimestamp > t.endTimestamp ? e : t : e).endTimestamp);
                let r = this.metadata
                  , i = {
                    contexts: {
                        ...this._contexts,
                        trace: this.getTraceContext()
                    },
                    spans: n,
                    start_timestamp: this.startTimestamp,
                    tags: this.tags,
                    timestamp: this.endTimestamp,
                    transaction: this.name,
                    type: "transaction",
                    sdkProcessingMetadata: {
                        ...r,
                        dynamicSamplingContext: this.getDynamicSamplingContext()
                    },
                    ...r.source && {
                        transaction_info: {
                            source: r.source
                        }
                    }
                }
                  , o = Object.keys(this._measurements).length > 0;
                return o && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Measurements] Adding measurements to transaction", JSON.stringify(this._measurements, void 0, 2)),
                i.measurements = this._measurements),
                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`[Tracing] Finishing ${this.op} transaction: ${this.name}.`),
                this._hub.captureEvent(i)
            }
            toContext() {
                let e = super.toContext();
                return (0,
                O.Jr)({
                    ...e,
                    name: this.name,
                    trimEnd: this._trimEnd
                })
            }
            updateWithContext(e) {
                return super.updateWithContext(e),
                this.name = e.name || "",
                this._trimEnd = e.trimEnd,
                this
            }
            getDynamicSamplingContext() {
                if (this._frozenDynamicSamplingContext)
                    return this._frozenDynamicSamplingContext;
                let e = this._hub || (0,
                g.Gd)()
                  , t = e.getClient();
                if (!t)
                    return {};
                let n = e.getScope()
                  , r = em(this.traceId, t, n)
                  , i = this.metadata.sampleRate;
                void 0 !== i && (r.sample_rate = `${i}`);
                let o = this.metadata.source;
                return o && "url" !== o && (r.transaction = this.name),
                void 0 !== this.sampled && (r.sampled = String(this.sampled)),
                r
            }
            setHub(e) {
                this._hub = e
            }
        }
        let tO = {
            idleTimeout: 1e3,
            finalTimeout: 3e4,
            heartbeatInterval: 5e3
        };
        class tN extends tk {
            constructor(e, t, n, r) {
                super(r),
                this._pushActivity = e,
                this._popActivity = t,
                this.transactionSpanId = n
            }
            add(e) {
                e.spanId !== this.transactionSpanId && (e.finish = t=>{
                    e.endTimestamp = "number" == typeof t ? t : (0,
                    e_.ph)(),
                    this._popActivity(e.spanId)
                }
                ,
                void 0 === e.endTimestamp && this._pushActivity(e.spanId)),
                super.add(e)
            }
        }
        class tC extends tD {
            constructor(e, t, n=tO.idleTimeout, r=tO.finalTimeout, i=tO.heartbeatInterval, o=!1) {
                super(e, t),
                this._idleHub = t,
                this._idleTimeout = n,
                this._finalTimeout = r,
                this._heartbeatInterval = i,
                this._onScope = o,
                this.activities = {},
                this._heartbeatCounter = 0,
                this._finished = !1,
                this._idleTimeoutCanceledPermanently = !1,
                this._beforeFinishCallbacks = [],
                this._finishReason = "externalFinish",
                o && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`Setting idle transaction on scope. Span ID: ${this.spanId}`),
                t.configureScope(e=>e.setSpan(this))),
                this._restartIdleTimeout(),
                setTimeout(()=>{
                    this._finished || (this.setStatus("deadline_exceeded"),
                    this._finishReason = "finalTimeout",
                    this.finish())
                }
                , this._finalTimeout)
            }
            finish(e=(0,
            e_.ph)()) {
                if (this._finished = !0,
                this.activities = {},
                "ui.action.click" === this.op && this.setTag("finishReason", this._finishReason),
                this.spanRecorder) {
                    for (let t of (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Tracing] finishing IdleTransaction", new Date(1e3 * e).toISOString(), this.op),
                    this._beforeFinishCallbacks))
                        t(this, e);
                    this.spanRecorder.spans = this.spanRecorder.spans.filter(t=>{
                        if (t.spanId === this.spanId)
                            return !0;
                        !t.endTimestamp && (t.endTimestamp = e,
                        t.setStatus("cancelled"),
                        ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Tracing] cancelling span since transaction ended early", JSON.stringify(t, void 0, 2)));
                        let n = t.startTimestamp < e
                          , r = (this._finalTimeout + this._idleTimeout) / 1e3
                          , i = t.endTimestamp - this.startTimestamp < r;
                        if ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) {
                            let o = JSON.stringify(t, void 0, 2);
                            n ? i || E.kg.log("[Tracing] discarding Span since it finished after Transaction final timeout", o) : E.kg.log("[Tracing] discarding Span since it happened after Transaction was finished", o)
                        }
                        return n && i
                    }
                    ),
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Tracing] flushing IdleTransaction")
                } else
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Tracing] No active IdleTransaction");
                if (this._onScope) {
                    let n = this._idleHub.getScope();
                    n.getTransaction() === this && n.setSpan(void 0)
                }
                return super.finish(e)
            }
            registerBeforeFinishCallback(e) {
                this._beforeFinishCallbacks.push(e)
            }
            initSpanRecorder(e) {
                if (!this.spanRecorder) {
                    let t = e=>{
                        this._finished || this._pushActivity(e)
                    }
                      , n = e=>{
                        this._finished || this._popActivity(e)
                    }
                    ;
                    this.spanRecorder = new tN(t,n,this.spanId,e),
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("Starting heartbeat"),
                    this._pingHeartbeat()
                }
                this.spanRecorder.add(this)
            }
            cancelIdleTimeout(e, {restartOnChildSpanChange: t}={
                restartOnChildSpanChange: !0
            }) {
                this._idleTimeoutCanceledPermanently = !1 === t,
                this._idleTimeoutID && (clearTimeout(this._idleTimeoutID),
                this._idleTimeoutID = void 0,
                0 === Object.keys(this.activities).length && this._idleTimeoutCanceledPermanently && (this._finishReason = "cancelled",
                this.finish(e)))
            }
            setFinishReason(e) {
                this._finishReason = e
            }
            _restartIdleTimeout(e) {
                this.cancelIdleTimeout(),
                this._idleTimeoutID = setTimeout(()=>{
                    this._finished || 0 !== Object.keys(this.activities).length || (this._finishReason = "idleTimeout",
                    this.finish(e))
                }
                , this._idleTimeout)
            }
            _pushActivity(e) {
                this.cancelIdleTimeout(void 0, {
                    restartOnChildSpanChange: !this._idleTimeoutCanceledPermanently
                }),
                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`[Tracing] pushActivity: ${e}`),
                this.activities[e] = !0,
                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Tracing] new activities count", Object.keys(this.activities).length)
            }
            _popActivity(e) {
                if (this.activities[e] && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`[Tracing] popActivity ${e}`),
                delete this.activities[e],
                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Tracing] new activities count", Object.keys(this.activities).length)),
                0 === Object.keys(this.activities).length) {
                    let t = (0,
                    e_.ph)();
                    this._idleTimeoutCanceledPermanently ? (this._finishReason = "cancelled",
                    this.finish(t)) : this._restartIdleTimeout(t + this._idleTimeout / 1e3)
                }
            }
            _beat() {
                if (this._finished)
                    return;
                let e = Object.keys(this.activities).join("");
                e === this._prevHeartbeatString ? this._heartbeatCounter++ : this._heartbeatCounter = 1,
                this._prevHeartbeatString = e,
                this._heartbeatCounter >= 3 ? (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Tracing] Transaction finished because of no change for 3 heart beats"),
                this.setStatus("deadline_exceeded"),
                this._finishReason = "heartbeatFailed",
                this.finish()) : this._pingHeartbeat()
            }
            _pingHeartbeat() {
                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`pinging Heartbeat -> current counter: ${this._heartbeatCounter}`),
                setTimeout(()=>{
                    this._beat()
                }
                , this._heartbeatInterval)
            }
        }
        function t$(e) {
            let t = e || (0,
            g.Gd)()
              , n = t.getScope();
            return n.getTransaction()
        }
        let tI = !1;
        function tP() {
            let e = t$();
            if (e) {
                let t = "internal_error";
                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`[Tracing] Transaction: ${t} -> Global error occured`),
                e.setStatus(t)
            }
        }
        function tA() {
            let e = this.getScope()
              , t = e.getSpan();
            return t ? {
                "sentry-trace": t.toTraceparent()
            } : {}
        }
        function tL(e, t, n) {
            var r;
            let i;
            return m(t) ? void 0 !== e.sampled ? (e.setMetadata({
                sampleRate: Number(e.sampled)
            }),
            e) : ("function" == typeof t.tracesSampler ? (i = t.tracesSampler(n),
            e.setMetadata({
                sampleRate: Number(i)
            })) : void 0 !== n.parentSampled ? i = n.parentSampled : void 0 !== t.tracesSampleRate ? (i = t.tracesSampleRate,
            e.setMetadata({
                sampleRate: Number(i)
            })) : (i = 1,
            e.setMetadata({
                sampleRate: i
            })),
            r = i,
            (0,
            V.i2)(r) || !("number" == typeof r || "boolean" == typeof r) ? (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`[Tracing] Given sample rate is invalid. Sample rate must be a boolean or a number between 0 and 1. Got ${JSON.stringify(r)} of type ${JSON.stringify(typeof r)}.`),
            1) : (r < 0 || r > 1) && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`[Tracing] Given sample rate is invalid. Sample rate must be between 0 and 1. Got ${r}.`),
            1)) ? (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("[Tracing] Discarding transaction because of invalid sample rate."),
            e.sampled = !1,
            e) : i ? (e.sampled = Math.random() < i,
            e.sampled) ? (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`[Tracing] starting ${e.op} transaction - ${e.name}`),
            e) : (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`[Tracing] Discarding transaction because it's not included in the random sample (sampling rate = ${Number(i)})`),
            e) : (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`[Tracing] Discarding transaction because ${"function" == typeof t.tracesSampler ? "tracesSampler returned 0 or false" : "a negative sampling decision was inherited or tracesSampleRate is set to 0"}`),
            e.sampled = !1,
            e) : (e.sampled = !1,
            e)
        }
        function tU(e, t) {
            let n = this.getClient()
              , r = n && n.getOptions() || {}
              , i = r.instrumenter || "sentry"
              , o = e.instrumenter || "sentry";
            i !== o && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.error(`A transaction was started with instrumenter=\`${o}\`, but the SDK is configured with the \`${i}\` instrumenter.
The transaction will not be sampled. Please use the ${i} instrumentation to start transactions.`),
            e.sampled = !1);
            let s = new tD(e,this);
            return (s = tL(s, r, {
                parentSampled: e.parentSampled,
                transactionContext: e,
                ...t
            })).sampled && s.initSpanRecorder(r._experiments && r._experiments.maxSpans),
            n && n.emit && n.emit("startTransaction", s),
            s
        }
        function tj(e, t, n, r, i, o, s) {
            let a = e.getClient()
              , l = a && a.getOptions() || {}
              , u = new tC(t,e,n,r,s,i);
            return (u = tL(u, l, {
                parentSampled: t.parentSampled,
                transactionContext: t,
                ...o
            })).sampled && u.initSpanRecorder(l._experiments && l._experiments.maxSpans),
            a && a.emit && a.emit("startTransaction", u),
            u
        }
        tP.tag = "sentry_tracingErrorCallback";
        let tB = B.n2
          , tY = (e,t,n)=>{
            let r, i;
            return o=>{
                t.value >= 0 && (o || n) && ((i = t.value - (r || 0)) || void 0 === r) && (r = t.value,
                t.delta = i,
                e(t))
            }
        }
          , tM = ()=>`v3-${Date.now()}-${Math.floor(Math.random() * (9e12 - 1)) + 1e12}`
          , tG = ()=>{
            let e = tB.performance.timing
              , t = tB.performance.navigation.type
              , n = {
                entryType: "navigation",
                startTime: 0,
                type: 2 == t ? "back_forward" : 1 === t ? "reload" : "navigate"
            };
            for (let r in e)
                "navigationStart" !== r && "toJSON" !== r && (n[r] = Math.max(e[r] - e.navigationStart, 0));
            return n
        }
          , tV = ()=>tB.__WEB_VITALS_POLYFILL__ ? tB.performance && (performance.getEntriesByType && performance.getEntriesByType("navigation")[0] || tG()) : tB.performance && performance.getEntriesByType && performance.getEntriesByType("navigation")[0]
          , tH = ()=>{
            let e = tV();
            return e && e.activationStart || 0
        }
          , tF = (e,t)=>{
            let n = tV()
              , r = "navigate";
            return n && (r = tB.document.prerendering || tH() > 0 ? "prerender" : n.type.replace(/_/g, "-")),
            {
                name: e,
                value: void 0 === t ? -1 : t,
                rating: "good",
                delta: 0,
                entries: [],
                id: tM(),
                navigationType: r
            }
        }
          , tz = (e,t,n)=>{
            try {
                if (PerformanceObserver.supportedEntryTypes.includes(e)) {
                    let r = new PerformanceObserver(e=>{
                        t(e.getEntries())
                    }
                    );
                    return r.observe(Object.assign({
                        type: e,
                        buffered: !0
                    }, n || {})),
                    r
                }
            } catch (i) {}
        }
          , tq = (e,t)=>{
            let n = r=>{
                ("pagehide" === r.type || "hidden" === tB.document.visibilityState) && (e(r),
                t && (removeEventListener("visibilitychange", n, !0),
                removeEventListener("pagehide", n, !0)))
            }
            ;
            addEventListener("visibilitychange", n, !0),
            addEventListener("pagehide", n, !0)
        }
          , tW = e=>{
            let t;
            let n = tF("CLS", 0)
              , r = 0
              , i = []
              , o = e=>{
                e.forEach(e=>{
                    if (!e.hadRecentInput) {
                        let o = i[0]
                          , s = i[i.length - 1];
                        r && 0 !== i.length && e.startTime - s.startTime < 1e3 && e.startTime - o.startTime < 5e3 ? (r += e.value,
                        i.push(e)) : (r = e.value,
                        i = [e]),
                        r > n.value && (n.value = r,
                        n.entries = i,
                        t && t())
                    }
                }
                )
            }
              , s = tz("layout-shift", o);
            if (s) {
                t = tY(e, n);
                let a = ()=>{
                    o(s.takeRecords()),
                    t(!0)
                }
                ;
                return tq(a),
                a
            }
        }
          , tJ = -1
          , tK = ()=>"hidden" !== tB.document.visibilityState || tB.document.prerendering ? 1 / 0 : 0
          , tX = ()=>{
            tq(({timeStamp: e})=>{
                tJ = e
            }
            , !0)
        }
          , tZ = ()=>(tJ < 0 && (tJ = tK(),
        tX()),
        {
            get firstHiddenTime() {
                return tJ
            }
        })
          , tQ = e=>{
            let t;
            let n = tZ()
              , r = tF("FID")
              , i = e=>{
                e.startTime < n.firstHiddenTime && (r.value = e.processingStart - e.startTime,
                r.entries.push(e),
                t(!0))
            }
              , o = e=>{
                e.forEach(i)
            }
              , s = tz("first-input", o);
            t = tY(e, r),
            s && tq(()=>{
                o(s.takeRecords()),
                s.disconnect()
            }
            , !0)
        }
          , t0 = {}
          , t1 = e=>{
            let t;
            let n = tZ()
              , r = tF("LCP")
              , i = e=>{
                let i = e[e.length - 1];
                if (i) {
                    let o = Math.max(i.startTime - tH(), 0);
                    o < n.firstHiddenTime && (r.value = o,
                    r.entries = [i],
                    t())
                }
            }
              , o = tz("largest-contentful-paint", i);
            if (o) {
                t = tY(e, r);
                let s = ()=>{
                    t0[r.id] || (i(o.takeRecords()),
                    o.disconnect(),
                    t0[r.id] = !0,
                    t(!0))
                }
                ;
                return ["keydown", "click"].forEach(e=>{
                    addEventListener(e, s, {
                        once: !0,
                        capture: !0
                    })
                }
                ),
                tq(s, !0),
                s
            }
        }
        ;
        function t2(e) {
            return "number" == typeof e && isFinite(e)
        }
        function t3(e, {startTimestamp: t, ...n}) {
            return t && e.startTimestamp > t && (e.startTimestamp = t),
            e.startChild({
                startTimestamp: t,
                ...n
            })
        }
        function t4(e) {
            return e / 1e3
        }
        function t5() {
            return tB && tB.addEventListener && tB.performance
        }
        let t6 = 0
          , t8 = {};
        function t9(e, t, n, r, i, o) {
            let s = o ? t[o] : t[`${n}End`]
              , a = t[`${n}Start`];
            a && s && t3(e, {
                op: "browser",
                description: i || n,
                startTimestamp: r + t4(a),
                endTimestamp: r + t4(s)
            })
        }
        let t7 = ["localhost", /^\/(?!\/)/]
          , ne = {
            traceFetch: !0,
            traceXHR: !0,
            enableHTTPTimings: !0,
            tracingOrigins: t7,
            tracePropagationTargets: t7
        };
        function nt(e) {
            let t = e.data.url
              , n = new PerformanceObserver(r=>{
                let i = r.getEntries();
                i.forEach(r=>{
                    if (("fetch" === r.initiatorType || "xmlhttprequest" === r.initiatorType) && r.name.endsWith(t)) {
                        let i = function(e) {
                            let {name: t, version: n} = function(e) {
                                let t = "unknown"
                                  , n = "unknown"
                                  , r = "";
                                for (let i of e) {
                                    if ("/" === i) {
                                        [t,n] = e.split("/");
                                        break
                                    }
                                    if (!isNaN(Number(i))) {
                                        t = "h" === r ? "http" : r,
                                        n = e.split(r)[1];
                                        break
                                    }
                                    r += i
                                }
                                return r === e && (t = r),
                                {
                                    name: t,
                                    version: n
                                }
                            }(e.nextHopProtocol)
                              , r = [];
                            return (r.push(["network.protocol.version", n], ["network.protocol.name", t]),
                            e_.Z1) ? [...r, ["http.request.redirect_start", nn(e.redirectStart)], ["http.request.fetch_start", nn(e.fetchStart)], ["http.request.domain_lookup_start", nn(e.domainLookupStart)], ["http.request.domain_lookup_end", nn(e.domainLookupEnd)], ["http.request.connect_start", nn(e.connectStart)], ["http.request.secure_connection_start", nn(e.secureConnectionStart)], ["http.request.connection_end", nn(e.connectEnd)], ["http.request.request_start", nn(e.requestStart)], ["http.request.response_start", nn(e.responseStart)], ["http.request.response_end", nn(e.responseEnd)]] : r
                        }(r);
                        i.forEach(t=>e.setData(...t)),
                        n.disconnect()
                    }
                }
                )
            }
            );
            n.observe({
                entryTypes: ["resource"]
            })
        }
        function nn(e) {
            return ((e_.Z1 || performance.timeOrigin) + e) / 1e3
        }
        function nr(e, t, n) {
            try {
                e.setRequestHeader("sentry-trace", t),
                n && e.setRequestHeader(ty, n)
            } catch (r) {}
        }
        let ni = {
            ...tO,
            markBackgroundTransactions: !0,
            routingInstrumentation: function(e, t=!0, n=!0) {
                let r;
                if (!tB || !tB.location) {
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("Could not initialize routing instrumentation due to invalid location");
                    return
                }
                let i = tB.location.href;
                t && (r = e({
                    name: tB.location.pathname,
                    startTimestamp: e_.Z1 ? e_.Z1 / 1e3 : void 0,
                    op: "pageload",
                    metadata: {
                        source: "url"
                    }
                })),
                n && J("history", ({to: t, from: n})=>{
                    if (void 0 === n && i && -1 !== i.indexOf(t)) {
                        i = void 0;
                        return
                    }
                    n !== t && (i = void 0,
                    r && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`[Tracing] Finishing current transaction with op: ${r.op}`),
                    r.finish()),
                    r = e({
                        name: tB.location.pathname,
                        op: "navigation",
                        metadata: {
                            source: "url"
                        }
                    }))
                }
                )
            },
            startTransactionOnLocationChange: !0,
            startTransactionOnPageLoad: !0,
            enableLongTask: !0,
            _experiments: {},
            ...ne
        };
        class no {
            constructor(e) {
                this.name = "BrowserTracing",
                this._hasSetTracePropagationTargets = !1,
                function() {
                    let e = (0,
                    g.cu)();
                    e.__SENTRY__ && (e.__SENTRY__.extensions = e.__SENTRY__.extensions || {},
                    e.__SENTRY__.extensions.startTransaction || (e.__SENTRY__.extensions.startTransaction = tU),
                    e.__SENTRY__.extensions.traceHeaders || (e.__SENTRY__.extensions.traceHeaders = tA),
                    tI || (tI = !0,
                    J("error", tP),
                    J("unhandledrejection", tP)))
                }(),
                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && (this._hasSetTracePropagationTargets = !!(e && (e.tracePropagationTargets || e.tracingOrigins))),
                this.options = {
                    ...ni,
                    ...e
                },
                void 0 !== this.options._experiments.enableLongTask && (this.options.enableLongTask = this.options._experiments.enableLongTask),
                e && !e.tracePropagationTargets && e.tracingOrigins && (this.options.tracePropagationTargets = e.tracingOrigins),
                this._collectWebVitals = function() {
                    let e = t5();
                    if (e && e_.Z1) {
                        e.mark && tB.performance.mark("sentry-tracing-init"),
                        tQ(e=>{
                            let t = e.entries.pop();
                            if (!t)
                                return;
                            let n = t4(e_.Z1)
                              , r = t4(t.startTime);
                            ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Measurements] Adding FID"),
                            t8.fid = {
                                value: e.value,
                                unit: "millisecond"
                            },
                            t8["mark.fid"] = {
                                value: n + r,
                                unit: "second"
                            }
                        }
                        );
                        let t = tW(e=>{
                            let t = e.entries.pop();
                            t && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Measurements] Adding CLS"),
                            t8.cls = {
                                value: e.value,
                                unit: ""
                            },
                            l = t)
                        }
                        )
                          , n = t1(e=>{
                            let t = e.entries.pop();
                            t && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Measurements] Adding LCP"),
                            t8.lcp = {
                                value: e.value,
                                unit: "millisecond"
                            },
                            a = t)
                        }
                        );
                        return ()=>{
                            t && t(),
                            n && n()
                        }
                    }
                    return ()=>void 0
                }(),
                this.options.enableLongTask && function() {
                    let e = e=>{
                        for (let t of e) {
                            let n = t$();
                            if (!n)
                                return;
                            let r = t4(e_.Z1 + t.startTime)
                              , i = t4(t.duration);
                            n.startChild({
                                description: "Main UI thread blocked",
                                op: "ui.long-task",
                                startTimestamp: r,
                                endTimestamp: r + i
                            })
                        }
                    }
                    ;
                    tz("longtask", e)
                }(),
                this.options._experiments.enableInteractions && function() {
                    let e = e=>{
                        for (let t of e) {
                            let n = t$();
                            if (!n)
                                return;
                            if ("click" === t.name) {
                                let r = t4(e_.Z1 + t.startTime)
                                  , i = t4(t.duration);
                                n.startChild({
                                    description: (0,
                                    eP.Rt)(t.target),
                                    op: `ui.interaction.${t.name}`,
                                    startTimestamp: r,
                                    endTimestamp: r + i
                                })
                            }
                        }
                    }
                    ;
                    tz("event", e, {
                        durationThreshold: 0
                    })
                }()
            }
            setupOnce(e, t) {
                this._getCurrentHub = t;
                let n = t()
                  , r = n.getClient()
                  , i = r && r.getOptions()
                  , {routingInstrumentation: o, startTransactionOnLocationChange: s, startTransactionOnPageLoad: a, markBackgroundTransactions: l, traceFetch: u, traceXHR: c, shouldCreateSpanForRequest: d, enableHTTPTimings: p, _experiments: h} = this.options
                  , f = i && i.tracePropagationTargets
                  , _ = f || this.options.tracePropagationTargets;
                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && this._hasSetTracePropagationTargets && f && E.kg.warn("[Tracing] The `tracePropagationTargets` option was set in the BrowserTracing integration and top level `Sentry.init`. The top level `Sentry.init` value is being used."),
                o(e=>{
                    let n = this._createRouteTransaction(e);
                    return this.options._experiments.onStartRouteTransaction && this.options._experiments.onStartRouteTransaction(n, e, t),
                    n
                }
                , a, s),
                l && (tB && tB.document ? tB.document.addEventListener("visibilitychange", ()=>{
                    let e = t$();
                    if (tB.document.hidden && e) {
                        let t = "cancelled";
                        ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`[Tracing] Transaction: ${t} -> since tab moved to the background, op: ${e.op}`),
                        e.status || e.setStatus(t),
                        e.setTag("visibilitychange", "document.hidden"),
                        e.finish()
                    }
                }
                ) : ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("[Tracing] Could not set up background tab detection due to lack of global document")),
                h.enableInteractions && this._registerInteractionListener(),
                function(e) {
                    let {traceFetch: t, traceXHR: n, tracePropagationTargets: r, tracingOrigins: i, shouldCreateSpanForRequest: o, enableHTTPTimings: s} = {
                        traceFetch: ne.traceFetch,
                        traceXHR: ne.traceXHR,
                        ...e
                    }
                      , a = "function" == typeof o ? o : e=>!0
                      , l = e=>(0,
                    x.U0)(e, r || i || t7)
                      , u = {};
                    t && J("fetch", e=>{
                        let t = function(e, t, n, r) {
                            if (!m() || !e.fetchData)
                                return;
                            let i = t(e.fetchData.url);
                            if (e.endTimestamp && i) {
                                let o = e.fetchData.__span;
                                if (!o)
                                    return;
                                let s = r[o];
                                if (s) {
                                    if (e.response) {
                                        s.setHttpStatus(e.response.status);
                                        let a = e.response && e.response.headers && e.response.headers.get("content-length")
                                          , l = parseInt(a);
                                        l > 0 && s.setData("http.response_content_length", l)
                                    } else
                                        e.error && s.setStatus("internal_error");
                                    s.finish(),
                                    delete r[o]
                                }
                                return
                            }
                            let u = (0,
                            g.Gd)()
                              , c = u.getScope()
                              , d = u.getClient()
                              , p = c.getSpan()
                              , {method: h, url: f} = e.fetchData
                              , _ = i && p ? p.startChild({
                                data: {
                                    url: f,
                                    type: "fetch",
                                    "http.method": h
                                },
                                description: `${h} ${f}`,
                                op: "http.client"
                            }) : void 0;
                            if (_ && (e.fetchData.__span = _.spanId,
                            r[_.spanId] = _),
                            n(e.fetchData.url) && d) {
                                let y = e.args[0];
                                e.args[1] = e.args[1] || {};
                                let v = e.args[1];
                                v.headers = function(e, t, n, r, i) {
                                    let o = i || n.getSpan()
                                      , s = o && o.transaction
                                      , {traceId: a, sampled: l, dsc: u} = n.getPropagationContext()
                                      , c = o ? o.toTraceparent() : tT(a, void 0, l)
                                      , d = s ? s.getDynamicSamplingContext() : u || em(a, t, n)
                                      , p = tS(d)
                                      , h = "undefined" != typeof Request && (0,
                                    V.V9)(e, Request) ? e.headers : r.headers;
                                    if (!h)
                                        return {
                                            "sentry-trace": c,
                                            baggage: p
                                        };
                                    if ("undefined" != typeof Headers && (0,
                                    V.V9)(h, Headers)) {
                                        let f = new Headers(h);
                                        return f.append("sentry-trace", c),
                                        p && f.append(ty, p),
                                        f
                                    }
                                    if (Array.isArray(h)) {
                                        let g = [...h, ["sentry-trace", c]];
                                        return p && g.push([ty, p]),
                                        g
                                    }
                                    {
                                        let m = "baggage"in h ? h.baggage : void 0
                                          , _ = [];
                                        return Array.isArray(m) ? _.push(...m) : m && _.push(m),
                                        p && _.push(p),
                                        {
                                            ...h,
                                            "sentry-trace": c,
                                            baggage: _.length > 0 ? _.join(",") : void 0
                                        }
                                    }
                                }(y, d, c, v, _)
                            }
                            return _
                        }(e, a, l, u);
                        s && t && nt(t)
                    }
                    ),
                    n && J("xhr", e=>{
                        let t = function(e, t, n, r) {
                            let i = e.xhr
                              , o = i && i[z];
                            if (!m() || i && i.__sentry_own_request__ || !i || !o)
                                return;
                            let s = t(o.url);
                            if (e.endTimestamp && s) {
                                let a = i.__sentry_xhr_span_id__;
                                if (!a)
                                    return;
                                let l = r[a];
                                l && (l.setHttpStatus(o.status_code),
                                l.finish(),
                                delete r[a]);
                                return
                            }
                            let u = (0,
                            g.Gd)()
                              , c = u.getScope()
                              , d = c.getSpan()
                              , p = s && d ? d.startChild({
                                data: {
                                    ...o.data,
                                    type: "xhr",
                                    "http.method": o.method,
                                    url: o.url
                                },
                                description: `${o.method} ${o.url}`,
                                op: "http.client"
                            }) : void 0;
                            if (p && (i.__sentry_xhr_span_id__ = p.spanId,
                            r[i.__sentry_xhr_span_id__] = p),
                            i.setRequestHeader && n(o.url)) {
                                if (p) {
                                    let h = p && p.transaction
                                      , f = h && h.getDynamicSamplingContext()
                                      , _ = tS(f);
                                    nr(i, p.toTraceparent(), _)
                                } else {
                                    let y = u.getClient()
                                      , {traceId: v, sampled: b, dsc: S} = c.getPropagationContext()
                                      , E = tT(v, void 0, b)
                                      , w = S || (y ? em(v, y, c) : void 0)
                                      , x = tS(w);
                                    nr(i, E, x)
                                }
                            }
                            return p
                        }(e, a, l, u);
                        s && t && nt(t)
                    }
                    )
                }({
                    traceFetch: u,
                    traceXHR: c,
                    tracePropagationTargets: _,
                    shouldCreateSpanForRequest: d,
                    enableHTTPTimings: p
                })
            }
            _createRouteTransaction(e) {
                if (!this._getCurrentHub) {
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`[Tracing] Did not create ${e.op} transaction because _getCurrentHub is invalid.`);
                    return
                }
                let t = this._getCurrentHub()
                  , {beforeNavigate: n, idleTimeout: r, finalTimeout: i, heartbeatInterval: o} = this.options
                  , s = "pageload" === e.op
                  , u = s ? ns("sentry-trace") : ""
                  , c = s ? ns("baggage") : ""
                  , {traceparentData: d, dynamicSamplingContext: p, propagationContext: h} = tx(u, c)
                  , f = {
                    ...e,
                    ...d,
                    metadata: {
                        ...e.metadata,
                        dynamicSamplingContext: d && !p ? {} : p
                    },
                    trimEnd: !0
                }
                  , g = "function" == typeof n ? n(f) : f
                  , m = void 0 === g ? {
                    ...f,
                    sampled: !1
                } : g;
                m.metadata = m.name !== f.name ? {
                    ...m.metadata,
                    source: "custom"
                } : m.metadata,
                this._latestRouteName = m.name,
                this._latestRouteSource = m.metadata && m.metadata.source,
                !1 === m.sampled && ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`[Tracing] Will not send ${m.op} transaction because of beforeNavigate.`),
                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`[Tracing] Starting ${m.op} transaction on scope`);
                let {location: _} = tB
                  , y = tj(t, m, r, i, !0, {
                    location: _
                }, o)
                  , v = t.getScope();
                return s && d ? v.setPropagationContext(h) : v.setPropagationContext({
                    traceId: y.traceId,
                    spanId: y.spanId,
                    parentSpanId: y.parentSpanId,
                    sampled: !!y.sampled
                }),
                y.registerBeforeFinishCallback(e=>{
                    this._collectWebVitals(),
                    function(e) {
                        let t, n;
                        let r = t5();
                        if (!r || !tB.performance.getEntries || !e_.Z1)
                            return;
                        ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Tracing] Adding & adjusting spans using Performance API");
                        let i = t4(e_.Z1)
                          , o = r.getEntries();
                        if (o.slice(t6).forEach(r=>{
                            let o = t4(r.startTime)
                              , s = t4(r.duration);
                            if ("navigation" !== e.op || !(i + o < e.startTimestamp))
                                switch (r.entryType) {
                                case "navigation":
                                    ["unloadEvent", "redirect", "domContentLoadedEvent", "loadEvent", "connect"].forEach(t=>{
                                        t9(e, r, t, i)
                                    }
                                    ),
                                    t9(e, r, "secureConnection", i, "TLS/SSL", "connectEnd"),
                                    t9(e, r, "fetch", i, "cache", "domainLookupStart"),
                                    t9(e, r, "domainLookup", i, "DNS"),
                                    t3(e, {
                                        op: "browser",
                                        description: "request",
                                        startTimestamp: i + t4(r.requestStart),
                                        endTimestamp: i + t4(r.responseEnd)
                                    }),
                                    t3(e, {
                                        op: "browser",
                                        description: "response",
                                        startTimestamp: i + t4(r.responseStart),
                                        endTimestamp: i + t4(r.responseEnd)
                                    }),
                                    t = i + t4(r.responseStart),
                                    n = i + t4(r.requestStart);
                                    break;
                                case "mark":
                                case "paint":
                                case "measure":
                                    {
                                        (function(e, t, n, r, i) {
                                            let o = i + n;
                                            t3(e, {
                                                description: t.name,
                                                endTimestamp: o + r,
                                                op: t.entryType,
                                                startTimestamp: o
                                            })
                                        }
                                        )(e, r, o, s, i);
                                        let a = tZ()
                                          , l = r.startTime < a.firstHiddenTime;
                                        "first-paint" === r.name && l && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Measurements] Adding FP"),
                                        t8.fp = {
                                            value: r.startTime,
                                            unit: "millisecond"
                                        }),
                                        "first-contentful-paint" === r.name && l && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Measurements] Adding FCP"),
                                        t8.fcp = {
                                            value: r.startTime,
                                            unit: "millisecond"
                                        });
                                        break
                                    }
                                case "resource":
                                    {
                                        let u = r.name.replace(tB.location.origin, "");
                                        (function(e, t, n, r, i, o) {
                                            if ("xmlhttprequest" === t.initiatorType || "fetch" === t.initiatorType)
                                                return;
                                            let s = {};
                                            "transferSize"in t && (s["http.response_transfer_size"] = t.transferSize),
                                            "encodedBodySize"in t && (s["http.response_content_length"] = t.encodedBodySize),
                                            "decodedBodySize"in t && (s["http.decoded_response_content_length"] = t.decodedBodySize),
                                            "renderBlockingStatus"in t && (s["resource.render_blocking_status"] = t.renderBlockingStatus);
                                            let a = o + r;
                                            t3(e, {
                                                description: n,
                                                endTimestamp: a + i,
                                                op: t.initiatorType ? `resource.${t.initiatorType}` : "resource.other",
                                                startTimestamp: a,
                                                data: s
                                            })
                                        }
                                        )(e, r, u, o, s, i)
                                    }
                                }
                        }
                        ),
                        t6 = Math.max(o.length - 1, 0),
                        function(e) {
                            let t = tB.navigator;
                            if (!t)
                                return;
                            let n = t.connection;
                            n && (n.effectiveType && e.setTag("effectiveConnectionType", n.effectiveType),
                            n.type && e.setTag("connectionType", n.type),
                            t2(n.rtt) && (t8["connection.rtt"] = {
                                value: n.rtt,
                                unit: "millisecond"
                            })),
                            t2(t.deviceMemory) && e.setTag("deviceMemory", `${t.deviceMemory} GB`),
                            t2(t.hardwareConcurrency) && e.setTag("hardwareConcurrency", String(t.hardwareConcurrency))
                        }(e),
                        "pageload" === e.op) {
                            "number" == typeof t && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Measurements] Adding TTFB"),
                            t8.ttfb = {
                                value: (t - e.startTimestamp) * 1e3,
                                unit: "millisecond"
                            },
                            "number" == typeof n && n <= t && (t8["ttfb.requestTime"] = {
                                value: (t - n) * 1e3,
                                unit: "millisecond"
                            })),
                            ["fcp", "fp", "lcp"].forEach(t=>{
                                if (!t8[t] || i >= e.startTimestamp)
                                    return;
                                let n = t8[t].value
                                  , r = i + t4(n)
                                  , o = Math.abs((r - e.startTimestamp) * 1e3);
                                ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log(`[Measurements] Normalized ${t} from ${n} to ${o} (${o - n})`),
                                t8[t].value = o
                            }
                            );
                            let s = t8["mark.fid"];
                            s && t8.fid && (t3(e, {
                                description: "first input delay",
                                endTimestamp: s.value + t4(t8.fid.value),
                                op: "ui.action",
                                startTimestamp: s.value
                            }),
                            delete t8["mark.fid"]),
                            "fcp"in t8 || delete t8.cls,
                            Object.keys(t8).forEach(t=>{
                                e.setMeasurement(t, t8[t].value, t8[t].unit)
                            }
                            ),
                            a && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Measurements] Adding LCP Data"),
                            a.element && e.setTag("lcp.element", (0,
                            eP.Rt)(a.element)),
                            a.id && e.setTag("lcp.id", a.id),
                            a.url && e.setTag("lcp.url", a.url.trim().slice(0, 200)),
                            e.setTag("lcp.size", a.size)),
                            l && l.sources && (("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.log("[Measurements] Adding CLS Data"),
                            l.sources.forEach((t,n)=>e.setTag(`cls.source.${n + 1}`, (0,
                            eP.Rt)(t.node))))
                        }
                        a = void 0,
                        l = void 0,
                        t8 = {}
                    }(e)
                }
                ),
                y
            }
            _registerInteractionListener() {
                let e;
                let t = ()=>{
                    let {idleTimeout: t, finalTimeout: n, heartbeatInterval: r} = this.options
                      , i = "ui.action.click"
                      , o = t$();
                    if (o && o.op && ["navigation", "pageload"].includes(o.op)) {
                        ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`[Tracing] Did not create ${i} transaction because a pageload or navigation transaction is in progress.`);
                        return
                    }
                    if (e && (e.setFinishReason("interactionInterrupted"),
                    e.finish(),
                    e = void 0),
                    !this._getCurrentHub) {
                        ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`[Tracing] Did not create ${i} transaction because _getCurrentHub is invalid.`);
                        return
                    }
                    if (!this._latestRouteName) {
                        ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn(`[Tracing] Did not create ${i} transaction because _latestRouteName is missing.`);
                        return
                    }
                    let s = this._getCurrentHub()
                      , {location: a} = tB
                      , l = {
                        name: this._latestRouteName,
                        op: i,
                        trimEnd: !0,
                        metadata: {
                            source: this._latestRouteSource || "url"
                        }
                    };
                    e = tj(s, l, t, n, !0, {
                        location: a
                    }, r)
                }
                ;
                ["click"].forEach(e=>{
                    addEventListener(e, t, {
                        once: !1,
                        capture: !0
                    })
                }
                )
            }
        }
        function ns(e) {
            let t = (0,
            eP.qT)(`meta[name=${e}]`);
            return t ? t.getAttribute("content") : void 0
        }
        function na(e, t, n={}) {
            return Array.isArray(t) ? nl(e, t, n) : function(e, t, n) {
                let r = r=>{
                    let i = t(r);
                    if (e.allowExclusionByUser) {
                        let o = i.find(t=>t.name === e.name);
                        if (!o)
                            return i
                    }
                    return nl(e, i, n)
                }
                ;
                return r
            }(e, t, n)
        }
        function nl(e, t, n) {
            let r = t.find(t=>t.name === e.name);
            if (r) {
                for (let[i,o] of Object.entries(n))
                    !function e(t, n, r) {
                        let i = n.match(/([a-z_]+)\.(.*)/i);
                        if (null === i)
                            t[n] = r;
                        else {
                            let o = t[i[1]];
                            e(o, i[2], r)
                        }
                    }(r, i, o);
                return t
            }
            return [...t, e]
        }
        var nu = n(34155)
          , nc = n(11163)
          , nd = n.n(nc);
        let np = {
            "routing.instrumentation": "next-router"
        }
          , nh = (0,
        g.Gd)().getClient();
        function nf(e, t=!0, n=!0) {
            let {route: r, params: i, sentryTrace: o, baggage: s} = function() {
                let e;
                let t = eC.document.getElementById("__NEXT_DATA__");
                if (t && t.innerHTML)
                    try {
                        e = JSON.parse(t.innerHTML)
                    } catch (n) {
                        ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("Could not extract __NEXT_DATA__")
                    }
                if (!e)
                    return {};
                let r = {}
                  , {page: i, query: o, props: s} = e;
                return r.route = i,
                r.params = o,
                s && s.pageProps && (r.sentryTrace = s.pageProps._sentryTraceData,
                r.baggage = s.pageProps._sentryBaggage),
                r
            }()
              , {traceparentData: a, dynamicSamplingContext: l, propagationContext: u} = tx(o, s);
            (0,
            g.Gd)().getScope().setPropagationContext(u),
            d = r || eC.location.pathname,
            t && (c = e({
                name: d,
                op: "pageload",
                tags: np,
                ...i && nh && nh.getOptions().sendDefaultPii && {
                    data: i
                },
                ...a,
                metadata: {
                    source: r ? "route" : "url",
                    dynamicSamplingContext: a && !l ? {} : l
                }
            })),
            n && nd().events.on("routeChangeStart", t=>{
                let n, r;
                let i = t.split(/[\?#]/, 1)[0]
                  , o = function(e) {
                    let t = (eC.__BUILD_MANIFEST || {}).sortedPages;
                    if (t)
                        return t.find(t=>{
                            let n = function(e) {
                                let t = e.split("/")
                                  , n = "";
                                t[t.length - 1].match(/^\[\[\.\.\..+\]\]$/) && (t.pop(),
                                n = "(?:/(.+?))?");
                                let r = t.map(e=>e.replace(/^\[\.\.\..+\]$/, "(.+?)").replace(/^\[.*\]$/, "([^/]+?)")).join("/");
                                return RegExp(`^${r}${n}(?:/)?$`)
                            }(t);
                            return e.match(n)
                        }
                        )
                }(i);
                o ? (n = o,
                r = "route") : (n = i,
                r = "url");
                let s = {
                    ...np,
                    from: d
                };
                d = n,
                c && c.finish();
                let a = e({
                    name: n,
                    op: "navigation",
                    tags: s,
                    metadata: {
                        source: r
                    }
                });
                if (a) {
                    let l = a.startChild({
                        op: "ui.nextjs.route-change",
                        description: "Next.js Route Change"
                    })
                      , u = ()=>{
                        l.finish(),
                        nd().events.off("routeChangeComplete", u)
                    }
                    ;
                    nd().events.on("routeChangeComplete", u)
                }
            }
            )
        }
        let ng = n.g
          , nm = n.g;
        var n_ = window;
        n_.__sentryRewritesTunnelPath__ = void 0,
        n_.SENTRY_RELEASE = {
            id: "Ds9Q8m_EHcbxBz-u-0mG3"
        },
        n_.__rewriteFramesAssetPrefixPath__ = "",
        function(e) {
            let t = ng.__sentryRewritesTunnelPath__;
            if (t && e.dsn) {
                let n = ei(e.dsn);
                if (!n)
                    return;
                let r = n.host.match(/^o(\d+)\.ingest\.sentry\.io$/);
                if (r) {
                    let i = r[1]
                      , o = `${t}?o=${i}&p=${n.projectId}`;
                    e.tunnel = o,
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.info(`Tunneling events to "${o}"`)
                } else
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("Provided DSN is not a Sentry SaaS DSN. Will not tunnel events.")
            }
        }(p = {
            dsn: "https://0fe0d6db57d347608f864249d1d29bdd@errortrace.dev/28",
            integrations: [new no({
                traceFetch: !1,
                tracePropagationTargets: []
            })],
            environment: "production"
        }),
        (h = p)._metadata = h._metadata || {},
        h._metadata.sdk = h._metadata.sdk || {
            name: "sentry.javascript.nextjs",
            packages: ["nextjs", "react"].map(e=>({
                name: `npm:@sentry/${e}`,
                version: S
            })),
            version: S
        },
        p.environment = p.environment || function(e) {
            let t = e ? nu.env.NEXT_PUBLIC_VERCEL_ENV : nu.env.VERCEL_ENV;
            return t ? `vercel-${t}` : void 0
        }(!0) || "production",
        function(e) {
            let t = e.integrations || []
              , n = nm.__rewriteFramesAssetPrefixPath__ || ""
              , r = new b({
                iteratee: e=>{
                    try {
                        let {origin: t} = new URL(e.filename);
                        e.filename = function(e) {
                            let t;
                            let n = e[0]
                              , r = 1;
                            for (; r < e.length; ) {
                                let i = e[r]
                                  , o = e[r + 1];
                                if (r += 2,
                                ("optionalAccess" === i || "optionalCall" === i) && null == n)
                                    return;
                                "access" === i || "optionalAccess" === i ? (t = n,
                                n = o(n)) : ("call" === i || "optionalCall" === i) && (n = o((...e)=>n.call(t, ...e)),
                                t = void 0)
                            }
                            return n
                        }([e, "access", e=>e.filename, "optionalAccess", e=>e.replace, "call", e=>e(t, "app://"), "access", e=>e.replace, "call", e=>e(n, "")])
                    } catch (r) {}
                    return e.filename && e.filename.startsWith("app:///_next") && (e.filename = decodeURI(e.filename)),
                    e.filename && e.filename.match(/^app:\/\/\/_next\/static\/chunks\/(main-|main-app-|polyfills-|webpack-|framework-|framework\.)[0-9a-f]+\.js$/) && (e.in_app = !1),
                    e
                }
            });
            if (t = na(r, t),
            ("undefined" == typeof __SENTRY_TRACING__ || __SENTRY_TRACING__) && m(e)) {
                let i = new no({
                    tracingOrigins: [...ne.tracingOrigins, /^(api\/)/],
                    routingInstrumentation: nf
                });
                t = na(i, t, {
                    "options.routingInstrumentation": nf
                })
            }
            e.integrations = t
        }(p),
        (f = p)._metadata = f._metadata || {},
        f._metadata.sdk = f._metadata.sdk || {
            name: "sentry.javascript.react",
            packages: [{
                name: "npm:@sentry/react",
                version: S
            }],
            version: S
        },
        function(e={}) {
            var t;
            void 0 === e.defaultIntegrations && (e.defaultIntegrations = tm),
            void 0 === e.release && ("string" == typeof __SENTRY_RELEASE__ && (e.release = __SENTRY_RELEASE__),
            eC.SENTRY_RELEASE && eC.SENTRY_RELEASE.id && (e.release = eC.SENTRY_RELEASE.id)),
            void 0 === e.autoSessionTracking && (e.autoSessionTracking = !0),
            void 0 === e.sendClientReports && (e.sendClientReports = !0);
            let n = {
                ...e,
                stackParser: Array.isArray(t = e.stackParser || tc) ? L(...t) : t,
                integrations: function(e) {
                    let t;
                    let n = e.defaultIntegrations || []
                      , r = e.integrations;
                    n.forEach(e=>{
                        e.isDefaultInstance = !0
                    }
                    ),
                    t = Array.isArray(r) ? [...n, ...r] : "function" == typeof r ? (0,
                    w.lE)(r(n)) : n;
                    let i = function(e) {
                        let t = {};
                        return e.forEach(e=>{
                            let {name: n} = e
                              , r = t[n];
                            r && !r.isDefaultInstance && e.isDefaultInstance || (t[n] = e)
                        }
                        ),
                        Object.keys(t).map(e=>t[e])
                    }(t)
                      , o = function(e, t) {
                        for (let n = 0; n < e.length; n++)
                            if (!0 === t(e[n]))
                                return n;
                        return -1
                    }(i, e=>"Debug" === e.name);
                    if (-1 !== o) {
                        let[s] = i.splice(o, 1);
                        i.push(s)
                    }
                    return i
                }(e),
                transport: e.transport || (M() ? tf : tg)
            };
            (function(e, t) {
                !0 === t.debug && ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__ ? E.kg.enable() : console.warn("[Sentry] Cannot initialize SDK with `debug` option using a non-debug bundle."));
                let n = (0,
                g.Gd)()
                  , r = n.getScope();
                r.update(t.initialScope);
                let i = new e(t);
                n.bindClient(i)
            }
            )(eV, n),
            e.autoSessionTracking && function() {
                if (void 0 === eC.document) {
                    ("undefined" == typeof __SENTRY_DEBUG__ || __SENTRY_DEBUG__) && E.kg.warn("Session tracking in non-browser environment with @sentry/browser is not supported.");
                    return
                }
                let e = (0,
                g.Gd)();
                e.captureSession && (t_(e),
                J("history", ({from: e, to: t})=>{
                    void 0 === e || e === t || t_((0,
                    g.Gd)())
                }
                ))
            }()
        }(f),
        (0,
        eN.e)(e=>{
            e.setTag("runtime", "browser");
            let t = e=>"transaction" === e.type && "/404" === e.transaction ? null : e;
            t.id = "NextClient404Filter",
            e.addEventProcessor(t)
        }
        )
    },
    14691: function(e, t, n) {
        "use strict";
        n.d(t, {
            a3: function() {
                return q
            },
            $G: function() {
                return z
            }
        });
        var r = n(85893)
          , i = n(67294);
        let o = {
            type: "logger",
            log(e) {
                this.output("log", e)
            },
            warn(e) {
                this.output("warn", e)
            },
            error(e) {
                this.output("error", e)
            },
            output(e, t) {
                console && console[e] && console[e].apply(console, t)
            }
        };
        class s {
            constructor(e) {
                let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : {};
                this.init(e, t)
            }
            init(e) {
                let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : {};
                this.prefix = t.prefix || "i18next:",
                this.logger = e || o,
                this.options = t,
                this.debug = t.debug
            }
            log() {
                for (var e = arguments.length, t = Array(e), n = 0; n < e; n++)
                    t[n] = arguments[n];
                return this.forward(t, "log", "", !0)
            }
            warn() {
                for (var e = arguments.length, t = Array(e), n = 0; n < e; n++)
                    t[n] = arguments[n];
                return this.forward(t, "warn", "", !0)
            }
            error() {
                for (var e = arguments.length, t = Array(e), n = 0; n < e; n++)
                    t[n] = arguments[n];
                return this.forward(t, "error", "")
            }
            deprecate() {
                for (var e = arguments.length, t = Array(e), n = 0; n < e; n++)
                    t[n] = arguments[n];
                return this.forward(t, "warn", "WARNING DEPRECATED: ", !0)
            }
            forward(e, t, n, r) {
                return r && !this.debug ? null : ("string" == typeof e[0] && (e[0] = `${n}${this.prefix} ${e[0]}`),
                this.logger[t](e))
            }
            create(e) {
                return new s(this.logger,{
                    prefix: `${this.prefix}:${e}:`,
                    ...this.options
                })
            }
            clone(e) {
                return (e = e || this.options).prefix = e.prefix || this.prefix,
                new s(this.logger,e)
            }
        }
        var a = new s;
        class l {
            constructor() {
                this.observers = {}
            }
            on(e, t) {
                return e.split(" ").forEach(e=>{
                    this.observers[e] = this.observers[e] || [],
                    this.observers[e].push(t)
                }
                ),
                this
            }
            off(e, t) {
                if (this.observers[e]) {
                    if (!t) {
                        delete this.observers[e];
                        return
                    }
                    this.observers[e] = this.observers[e].filter(e=>e !== t)
                }
            }
            emit(e) {
                for (var t = arguments.length, n = Array(t > 1 ? t - 1 : 0), r = 1; r < t; r++)
                    n[r - 1] = arguments[r];
                if (this.observers[e]) {
                    let i = [].concat(this.observers[e]);
                    i.forEach(e=>{
                        e(...n)
                    }
                    )
                }
                if (this.observers["*"]) {
                    let o = [].concat(this.observers["*"]);
                    o.forEach(t=>{
                        t.apply(t, [e, ...n])
                    }
                    )
                }
            }
        }
        function u() {
            let e, t;
            let n = new Promise((n,r)=>{
                e = n,
                t = r
            }
            );
            return n.resolve = e,
            n.reject = t,
            n
        }
        function c(e) {
            return null == e ? "" : "" + e
        }
        function d(e, t, n) {
            function r(e) {
                return e && e.indexOf("###") > -1 ? e.replace(/###/g, ".") : e
            }
            function i() {
                return !e || "string" == typeof e
            }
            let o = "string" != typeof t ? [].concat(t) : t.split(".");
            for (; o.length > 1; ) {
                if (i())
                    return {};
                let s = r(o.shift());
                !e[s] && n && (e[s] = new n),
                e = Object.prototype.hasOwnProperty.call(e, s) ? e[s] : {}
            }
            return i() ? {} : {
                obj: e,
                k: r(o.shift())
            }
        }
        function p(e, t, n) {
            let {obj: r, k: i} = d(e, t, Object);
            r[i] = n
        }
        function h(e, t) {
            let {obj: n, k: r} = d(e, t);
            if (n)
                return n[r]
        }
        function f(e) {
            return e.replace(/[\-\[\]\/\{\}\(\)\*\+\?\.\\\^\$\|]/g, "\\$&")
        }
        var g = {
            "&": "&amp;",
            "<": "&lt;",
            ">": "&gt;",
            '"': "&quot;",
            "'": "&#39;",
            "/": "&#x2F;"
        };
        function m(e) {
            return "string" == typeof e ? e.replace(/[&<>"'\/]/g, e=>g[e]) : e
        }
        let _ = [" ", ",", "?", "!", ";"];
        function y(e, t) {
            let n = arguments.length > 2 && void 0 !== arguments[2] ? arguments[2] : ".";
            if (!e)
                return;
            if (e[t])
                return e[t];
            let r = t.split(n)
              , i = e;
            for (let o = 0; o < r.length; ++o) {
                if (!i || "string" == typeof i[r[o]] && o + 1 < r.length)
                    return;
                if (void 0 === i[r[o]]) {
                    let s = 2
                      , a = r.slice(o, o + s).join(n)
                      , l = i[a];
                    for (; void 0 === l && r.length > o + s; )
                        s++,
                        l = i[a = r.slice(o, o + s).join(n)];
                    if (void 0 === l)
                        return;
                    if (null === l)
                        return null;
                    if (t.endsWith(a)) {
                        if ("string" == typeof l)
                            return l;
                        if (a && "string" == typeof l[a])
                            return l[a]
                    }
                    let u = r.slice(o + s).join(n);
                    if (u)
                        return y(l, u, n);
                    return
                }
                i = i[r[o]]
            }
            return i
        }
        function v(e) {
            return e && e.indexOf("_") > 0 ? e.replace("_", "-") : e
        }
        class b extends l {
            constructor(e) {
                let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : {
                    ns: ["translation"],
                    defaultNS: "translation"
                };
                super(),
                this.data = e || {},
                this.options = t,
                void 0 === this.options.keySeparator && (this.options.keySeparator = "."),
                void 0 === this.options.ignoreJSONStructure && (this.options.ignoreJSONStructure = !0)
            }
            addNamespaces(e) {
                0 > this.options.ns.indexOf(e) && this.options.ns.push(e)
            }
            removeNamespaces(e) {
                let t = this.options.ns.indexOf(e);
                t > -1 && this.options.ns.splice(t, 1)
            }
            getResource(e, t, n) {
                let r = arguments.length > 3 && void 0 !== arguments[3] ? arguments[3] : {}
                  , i = void 0 !== r.keySeparator ? r.keySeparator : this.options.keySeparator
                  , o = void 0 !== r.ignoreJSONStructure ? r.ignoreJSONStructure : this.options.ignoreJSONStructure
                  , s = [e, t];
                n && "string" != typeof n && (s = s.concat(n)),
                n && "string" == typeof n && (s = s.concat(i ? n.split(i) : n)),
                e.indexOf(".") > -1 && (s = e.split("."));
                let a = h(this.data, s);
                return a || !o || "string" != typeof n ? a : y(this.data && this.data[e] && this.data[e][t], n, i)
            }
            addResource(e, t, n, r) {
                let i = arguments.length > 4 && void 0 !== arguments[4] ? arguments[4] : {
                    silent: !1
                }
                  , o = void 0 !== i.keySeparator ? i.keySeparator : this.options.keySeparator
                  , s = [e, t];
                n && (s = s.concat(o ? n.split(o) : n)),
                e.indexOf(".") > -1 && (s = e.split("."),
                r = t,
                t = s[1]),
                this.addNamespaces(t),
                p(this.data, s, r),
                i.silent || this.emit("added", e, t, n, r)
            }
            addResources(e, t, n) {
                let r = arguments.length > 3 && void 0 !== arguments[3] ? arguments[3] : {
                    silent: !1
                };
                for (let i in n)
                    ("string" == typeof n[i] || "[object Array]" === Object.prototype.toString.apply(n[i])) && this.addResource(e, t, i, n[i], {
                        silent: !0
                    });
                r.silent || this.emit("added", e, t, n)
            }
            addResourceBundle(e, t, n, r, i) {
                let o = arguments.length > 5 && void 0 !== arguments[5] ? arguments[5] : {
                    silent: !1
                }
                  , s = [e, t];
                e.indexOf(".") > -1 && (s = e.split("."),
                r = n,
                n = t,
                t = s[1]),
                this.addNamespaces(t);
                let a = h(this.data, s) || {};
                r ? function e(t, n, r) {
                    for (let i in n)
                        "__proto__" !== i && "constructor" !== i && (i in t ? "string" == typeof t[i] || t[i]instanceof String || "string" == typeof n[i] || n[i]instanceof String ? r && (t[i] = n[i]) : e(t[i], n[i], r) : t[i] = n[i]);
                    return t
                }(a, n, i) : a = {
                    ...a,
                    ...n
                },
                p(this.data, s, a),
                o.silent || this.emit("added", e, t, n)
            }
            removeResourceBundle(e, t) {
                this.hasResourceBundle(e, t) && delete this.data[e][t],
                this.removeNamespaces(t),
                this.emit("removed", e, t)
            }
            hasResourceBundle(e, t) {
                return void 0 !== this.getResource(e, t)
            }
            getResourceBundle(e, t) {
                return (t || (t = this.options.defaultNS),
                "v1" === this.options.compatibilityAPI) ? {
                    ...this.getResource(e, t)
                } : this.getResource(e, t)
            }
            getDataByLanguage(e) {
                return this.data[e]
            }
            hasLanguageSomeTranslations(e) {
                let t = this.getDataByLanguage(e)
                  , n = t && Object.keys(t) || [];
                return !!n.find(e=>t[e] && Object.keys(t[e]).length > 0)
            }
            toJSON() {
                return this.data
            }
        }
        var S = {
            processors: {},
            addPostProcessor(e) {
                this.processors[e.name] = e
            },
            handle(e, t, n, r, i) {
                return e.forEach(e=>{
                    this.processors[e] && (t = this.processors[e].process(t, n, r, i))
                }
                ),
                t
            }
        };
        let E = {};
        class w extends l {
            constructor(e) {
                let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : {};
                super(),
                function(e, t, n) {
                    e.forEach(e=>{
                        t[e] && (n[e] = t[e])
                    }
                    )
                }(["resourceStore", "languageUtils", "pluralResolver", "interpolator", "backendConnector", "i18nFormat", "utils"], e, this),
                this.options = t,
                void 0 === this.options.keySeparator && (this.options.keySeparator = "."),
                this.logger = a.create("translator")
            }
            changeLanguage(e) {
                e && (this.language = e)
            }
            exists(e) {
                let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : {
                    interpolation: {}
                };
                if (null == e)
                    return !1;
                let n = this.resolve(e, t);
                return n && void 0 !== n.res
            }
            extractFromKey(e, t) {
                let n = void 0 !== t.nsSeparator ? t.nsSeparator : this.options.nsSeparator;
                void 0 === n && (n = ":");
                let r = void 0 !== t.keySeparator ? t.keySeparator : this.options.keySeparator
                  , i = t.ns || this.options.defaultNS || []
                  , o = n && e.indexOf(n) > -1
                  , s = !this.options.userDefinedKeySeparator && !t.keySeparator && !this.options.userDefinedNsSeparator && !t.nsSeparator && !function(e, t, n) {
                    t = t || "",
                    n = n || "";
                    let r = _.filter(e=>0 > t.indexOf(e) && 0 > n.indexOf(e));
                    if (0 === r.length)
                        return !0;
                    let i = RegExp(`(${r.map(e=>"?" === e ? "\\?" : e).join("|")})`)
                      , o = !i.test(e);
                    if (!o) {
                        let s = e.indexOf(n);
                        s > 0 && !i.test(e.substring(0, s)) && (o = !0)
                    }
                    return o
                }(e, n, r);
                if (o && !s) {
                    let a = e.match(this.interpolator.nestingRegexp);
                    if (a && a.length > 0)
                        return {
                            key: e,
                            namespaces: i
                        };
                    let l = e.split(n);
                    (n !== r || n === r && this.options.ns.indexOf(l[0]) > -1) && (i = l.shift()),
                    e = l.join(r)
                }
                return "string" == typeof i && (i = [i]),
                {
                    key: e,
                    namespaces: i
                }
            }
            translate(e, t, n) {
                if ("object" != typeof t && this.options.overloadTranslationOptionHandler && (t = this.options.overloadTranslationOptionHandler(arguments)),
                "object" == typeof t && (t = {
                    ...t
                }),
                t || (t = {}),
                null == e)
                    return "";
                Array.isArray(e) || (e = [String(e)]);
                let r = void 0 !== t.returnDetails ? t.returnDetails : this.options.returnDetails
                  , i = void 0 !== t.keySeparator ? t.keySeparator : this.options.keySeparator
                  , {key: o, namespaces: s} = this.extractFromKey(e[e.length - 1], t)
                  , a = s[s.length - 1]
                  , l = t.lng || this.language
                  , u = t.appendNamespaceToCIMode || this.options.appendNamespaceToCIMode;
                if (l && "cimode" === l.toLowerCase()) {
                    if (u) {
                        let c = t.nsSeparator || this.options.nsSeparator;
                        return r ? {
                            res: `${a}${c}${o}`,
                            usedKey: o,
                            exactUsedKey: o,
                            usedLng: l,
                            usedNS: a
                        } : `${a}${c}${o}`
                    }
                    return r ? {
                        res: o,
                        usedKey: o,
                        exactUsedKey: o,
                        usedLng: l,
                        usedNS: a
                    } : o
                }
                let d = this.resolve(e, t)
                  , p = d && d.res
                  , h = d && d.usedKey || o
                  , f = d && d.exactUsedKey || o
                  , g = Object.prototype.toString.apply(p)
                  , m = void 0 !== t.joinArrays ? t.joinArrays : this.options.joinArrays
                  , _ = !this.i18nFormat || this.i18nFormat.handleAsObject
                  , y = "string" != typeof p && "boolean" != typeof p && "number" != typeof p;
                if (_ && p && y && 0 > ["[object Number]", "[object Function]", "[object RegExp]"].indexOf(g) && !("string" == typeof m && "[object Array]" === g)) {
                    if (!t.returnObjects && !this.options.returnObjects) {
                        this.options.returnedObjectHandler || this.logger.warn("accessing an object - but returnObjects options is not enabled!");
                        let v = this.options.returnedObjectHandler ? this.options.returnedObjectHandler(h, p, {
                            ...t,
                            ns: s
                        }) : `key '${o} (${this.language})' returned an object instead of string.`;
                        return r ? (d.res = v,
                        d) : v
                    }
                    if (i) {
                        let b = "[object Array]" === g
                          , S = b ? [] : {}
                          , E = b ? f : h;
                        for (let x in p)
                            if (Object.prototype.hasOwnProperty.call(p, x)) {
                                let T = `${E}${i}${x}`;
                                S[x] = this.translate(T, {
                                    ...t,
                                    joinArrays: !1,
                                    ns: s
                                }),
                                S[x] === T && (S[x] = p[x])
                            }
                        p = S
                    }
                } else if (_ && "string" == typeof m && "[object Array]" === g)
                    (p = p.join(m)) && (p = this.extendTranslation(p, e, t, n));
                else {
                    let k = !1
                      , R = !1
                      , D = void 0 !== t.count && "string" != typeof t.count
                      , O = w.hasDefaultValue(t)
                      , N = D ? this.pluralResolver.getSuffix(l, t.count, t) : ""
                      , C = t.ordinal && D ? this.pluralResolver.getSuffix(l, t.count, {
                        ordinal: !1
                    }) : ""
                      , $ = t[`defaultValue ${N}`] || t[`defaultValue ${C}`] || t.defaultValue;
                    !this.isValidLookup(p) && O && (k = !0,
                    p = $),
                    this.isValidLookup(p) || (R = !0,
                    p = o);
                    let I = t.missingKeyNoValueFallbackToKey || this.options.missingKeyNoValueFallbackToKey
                      , P = I && R ? void 0 : p
                      , A = O && $ !== p && this.options.updateMissing;
                    if (R || k || A) {
                        if (this.logger.log(A ? "updateKey" : "missingKey", l, a, o, A ? $ : p),
                        i) {
                            let L = this.resolve(o, {
                                ...t,
                                keySeparator: !1
                            });
                            L && L.res && this.logger.warn("Seems the loaded translations were in flat JSON format instead of nested. Either set keySeparator: false on init or make sure your translations are published in nested format.")
                        }
                        let U = []
                          , j = this.languageUtils.getFallbackCodes(this.options.fallbackLng, t.lng || this.language);
                        if ("fallback" === this.options.saveMissingTo && j && j[0])
                            for (let B = 0; B < j.length; B++)
                                U.push(j[B]);
                        else
                            "all" === this.options.saveMissingTo ? U = this.languageUtils.toResolveHierarchy(t.lng || this.language) : U.push(t.lng || this.language);
                        let Y = (e,n,r)=>{
                            let i = O && r !== p ? r : P;
                            this.options.missingKeyHandler ? this.options.missingKeyHandler(e, a, n, i, A, t) : this.backendConnector && this.backendConnector.saveMissing && this.backendConnector.saveMissing(e, a, n, i, A, t),
                            this.emit("missingKey", e, a, n, p)
                        }
                        ;
                        this.options.saveMissing && (this.options.saveMissingPlurals && D ? U.forEach(e=>{
                            this.pluralResolver.getSuffixes(e, t).forEach(n=>{
                                Y([e], o + n, t[`defaultValue ${n}`] || $)
                            }
                            )
                        }
                        ) : Y(U, o, $))
                    }
                    p = this.extendTranslation(p, e, t, d, n),
                    R && p === o && this.options.appendNamespaceToMissingKey && (p = `${a}:${o}`),
                    (R || k) && this.options.parseMissingKeyHandler && (p = "v1" !== this.options.compatibilityAPI ? this.options.parseMissingKeyHandler(this.options.appendNamespaceToMissingKey ? `${a}:${o}` : o, k ? p : void 0) : this.options.parseMissingKeyHandler(p))
                }
                return r ? (d.res = p,
                d) : p
            }
            extendTranslation(e, t, n, r, i) {
                var o = this;
                if (this.i18nFormat && this.i18nFormat.parse)
                    e = this.i18nFormat.parse(e, {
                        ...this.options.interpolation.defaultVariables,
                        ...n
                    }, n.lng || this.language || r.usedLng, r.usedNS, r.usedKey, {
                        resolved: r
                    });
                else if (!n.skipInterpolation) {
                    let s;
                    n.interpolation && this.interpolator.init({
                        ...n,
                        interpolation: {
                            ...this.options.interpolation,
                            ...n.interpolation
                        }
                    });
                    let a = "string" == typeof e && (n && n.interpolation && void 0 !== n.interpolation.skipOnVariables ? n.interpolation.skipOnVariables : this.options.interpolation.skipOnVariables);
                    if (a) {
                        let l = e.match(this.interpolator.nestingRegexp);
                        s = l && l.length
                    }
                    let u = n.replace && "string" != typeof n.replace ? n.replace : n;
                    if (this.options.interpolation.defaultVariables && (u = {
                        ...this.options.interpolation.defaultVariables,
                        ...u
                    }),
                    e = this.interpolator.interpolate(e, u, n.lng || this.language, n),
                    a) {
                        let c = e.match(this.interpolator.nestingRegexp)
                          , d = c && c.length;
                        s < d && (n.nest = !1)
                    }
                    !n.lng && "v1" !== this.options.compatibilityAPI && r && r.res && (n.lng = r.usedLng),
                    !1 !== n.nest && (e = this.interpolator.nest(e, function() {
                        for (var e = arguments.length, r = Array(e), s = 0; s < e; s++)
                            r[s] = arguments[s];
                        return i && i[0] === r[0] && !n.context ? (o.logger.warn(`It seems you are nesting recursively key: ${r[0]} in key: ${t[0]}`),
                        null) : o.translate(...r, t)
                    }, n)),
                    n.interpolation && this.interpolator.reset()
                }
                let p = n.postProcess || this.options.postProcess
                  , h = "string" == typeof p ? [p] : p;
                return null != e && h && h.length && !1 !== n.applyPostProcessor && (e = S.handle(h, e, t, this.options && this.options.postProcessPassResolved ? {
                    i18nResolved: r,
                    ...n
                } : n, this)),
                e
            }
            resolve(e) {
                let t, n, r, i, o, s = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : {};
                return "string" == typeof e && (e = [e]),
                e.forEach(e=>{
                    if (this.isValidLookup(t))
                        return;
                    let a = this.extractFromKey(e, s)
                      , l = a.key;
                    n = l;
                    let u = a.namespaces;
                    this.options.fallbackNS && (u = u.concat(this.options.fallbackNS));
                    let c = void 0 !== s.count && "string" != typeof s.count
                      , d = c && !s.ordinal && 0 === s.count && this.pluralResolver.shouldUseIntlApi()
                      , p = void 0 !== s.context && ("string" == typeof s.context || "number" == typeof s.context) && "" !== s.context
                      , h = s.lngs ? s.lngs : this.languageUtils.toResolveHierarchy(s.lng || this.language, s.fallbackLng);
                    u.forEach(e=>{
                        this.isValidLookup(t) || (o = e,
                        !E[`${h[0]}-${e}`] && this.utils && this.utils.hasLoadedNamespace && !this.utils.hasLoadedNamespace(o) && (E[`${h[0]}-${e}`] = !0,
                        this.logger.warn(`key "${n}" for languages "${h.join(", ")}" won't get resolved as namespace "${o}" was not yet loaded`, "This means something IS WRONG in your setup. You access the t function before i18next.init / i18next.loadNamespace / i18next.changeLanguage was done. Wait for the callback or Promise to resolve before accessing it!!!")),
                        h.forEach(n=>{
                            let o;
                            if (this.isValidLookup(t))
                                return;
                            i = n;
                            let a = [l];
                            if (this.i18nFormat && this.i18nFormat.addLookupKeys)
                                this.i18nFormat.addLookupKeys(a, l, n, e, s);
                            else {
                                let u;
                                c && (u = this.pluralResolver.getSuffix(n, s.count, s));
                                let h = `${this.options.pluralSeparator}zero`
                                  , f = `${this.options.pluralSeparator}ordinal ${this.options.pluralSeparator}`;
                                if (c && (a.push(l + u),
                                s.ordinal && 0 === u.indexOf(f) && a.push(l + u.replace(f, this.options.pluralSeparator)),
                                d && a.push(l + h)),
                                p) {
                                    let g = `${l}${this.options.contextSeparator}${s.context}`;
                                    a.push(g),
                                    c && (a.push(g + u),
                                    s.ordinal && 0 === u.indexOf(f) && a.push(g + u.replace(f, this.options.pluralSeparator)),
                                    d && a.push(g + h))
                                }
                            }
                            for (; o = a.pop(); )
                                this.isValidLookup(t) || (r = o,
                                t = this.getResource(n, e, o, s))
                        }
                        ))
                    }
                    )
                }
                ),
                {
                    res: t,
                    usedKey: n,
                    exactUsedKey: r,
                    usedLng: i,
                    usedNS: o
                }
            }
            isValidLookup(e) {
                return void 0 !== e && !(!this.options.returnNull && null === e) && !(!this.options.returnEmptyString && "" === e)
            }
            getResource(e, t, n) {
                let r = arguments.length > 3 && void 0 !== arguments[3] ? arguments[3] : {};
                return this.i18nFormat && this.i18nFormat.getResource ? this.i18nFormat.getResource(e, t, n, r) : this.resourceStore.getResource(e, t, n, r)
            }
            static hasDefaultValue(e) {
                let t = "defaultValue";
                for (let n in e)
                    if (Object.prototype.hasOwnProperty.call(e, n) && t === n.substring(0, t.length) && void 0 !== e[n])
                        return !0;
                return !1
            }
        }
        function x(e) {
            return e.charAt(0).toUpperCase() + e.slice(1)
        }
        class T {
            constructor(e) {
                this.options = e,
                this.supportedLngs = this.options.supportedLngs || !1,
                this.logger = a.create("languageUtils")
            }
            getScriptPartFromCode(e) {
                if (!(e = v(e)) || 0 > e.indexOf("-"))
                    return null;
                let t = e.split("-");
                return 2 === t.length ? null : (t.pop(),
                "x" === t[t.length - 1].toLowerCase()) ? null : this.formatLanguageCode(t.join("-"))
            }
            getLanguagePartFromCode(e) {
                if (!(e = v(e)) || 0 > e.indexOf("-"))
                    return e;
                let t = e.split("-");
                return this.formatLanguageCode(t[0])
            }
            formatLanguageCode(e) {
                if ("string" == typeof e && e.indexOf("-") > -1) {
                    let t = ["hans", "hant", "latn", "cyrl", "cans", "mong", "arab"]
                      , n = e.split("-");
                    return this.options.lowerCaseLng ? n = n.map(e=>e.toLowerCase()) : 2 === n.length ? (n[0] = n[0].toLowerCase(),
                    n[1] = n[1].toUpperCase(),
                    t.indexOf(n[1].toLowerCase()) > -1 && (n[1] = x(n[1].toLowerCase()))) : 3 === n.length && (n[0] = n[0].toLowerCase(),
                    2 === n[1].length && (n[1] = n[1].toUpperCase()),
                    "sgn" !== n[0] && 2 === n[2].length && (n[2] = n[2].toUpperCase()),
                    t.indexOf(n[1].toLowerCase()) > -1 && (n[1] = x(n[1].toLowerCase())),
                    t.indexOf(n[2].toLowerCase()) > -1 && (n[2] = x(n[2].toLowerCase()))),
                    n.join("-")
                }
                return this.options.cleanCode || this.options.lowerCaseLng ? e.toLowerCase() : e
            }
            isSupportedCode(e) {
                return ("languageOnly" === this.options.load || this.options.nonExplicitSupportedLngs) && (e = this.getLanguagePartFromCode(e)),
                !this.supportedLngs || !this.supportedLngs.length || this.supportedLngs.indexOf(e) > -1
            }
            getBestMatchFromCodes(e) {
                let t;
                return e ? (e.forEach(e=>{
                    if (t)
                        return;
                    let n = this.formatLanguageCode(e);
                    (!this.options.supportedLngs || this.isSupportedCode(n)) && (t = n)
                }
                ),
                !t && this.options.supportedLngs && e.forEach(e=>{
                    if (t)
                        return;
                    let n = this.getLanguagePartFromCode(e);
                    if (this.isSupportedCode(n))
                        return t = n;
                    t = this.options.supportedLngs.find(e=>{
                        if (e === n || !(0 > e.indexOf("-") && 0 > n.indexOf("-")) && 0 === e.indexOf(n))
                            return e
                    }
                    )
                }
                ),
                t || (t = this.getFallbackCodes(this.options.fallbackLng)[0]),
                t) : null
            }
            getFallbackCodes(e, t) {
                if (!e)
                    return [];
                if ("function" == typeof e && (e = e(t)),
                "string" == typeof e && (e = [e]),
                "[object Array]" === Object.prototype.toString.apply(e))
                    return e;
                if (!t)
                    return e.default || [];
                let n = e[t];
                return n || (n = e[this.getScriptPartFromCode(t)]),
                n || (n = e[this.formatLanguageCode(t)]),
                n || (n = e[this.getLanguagePartFromCode(t)]),
                n || (n = e.default),
                n || []
            }
            toResolveHierarchy(e, t) {
                let n = this.getFallbackCodes(t || this.options.fallbackLng || [], e)
                  , r = []
                  , i = e=>{
                    e && (this.isSupportedCode(e) ? r.push(e) : this.logger.warn(`rejecting language code not found in supportedLngs: ${e}`))
                }
                ;
                return "string" == typeof e && (e.indexOf("-") > -1 || e.indexOf("_") > -1) ? ("languageOnly" !== this.options.load && i(this.formatLanguageCode(e)),
                "languageOnly" !== this.options.load && "currentOnly" !== this.options.load && i(this.getScriptPartFromCode(e)),
                "currentOnly" !== this.options.load && i(this.getLanguagePartFromCode(e))) : "string" == typeof e && i(this.formatLanguageCode(e)),
                n.forEach(e=>{
                    0 > r.indexOf(e) && i(this.formatLanguageCode(e))
                }
                ),
                r
            }
        }
        let k = [{
            lngs: ["ach", "ak", "am", "arn", "br", "fil", "gun", "ln", "mfe", "mg", "mi", "oc", "pt", "pt-BR", "tg", "tl", "ti", "tr", "uz", "wa"],
            nr: [1, 2],
            fc: 1
        }, {
            lngs: ["af", "an", "ast", "az", "bg", "bn", "ca", "da", "de", "dev", "el", "en", "eo", "es", "et", "eu", "fi", "fo", "fur", "fy", "gl", "gu", "ha", "hi", "hu", "hy", "ia", "it", "kk", "kn", "ku", "lb", "mai", "ml", "mn", "mr", "nah", "nap", "nb", "ne", "nl", "nn", "no", "nso", "pa", "pap", "pms", "ps", "pt-PT", "rm", "sco", "se", "si", "so", "son", "sq", "sv", "sw", "ta", "te", "tk", "ur", "yo"],
            nr: [1, 2],
            fc: 2
        }, {
            lngs: ["ay", "bo", "cgg", "fa", "ht", "id", "ja", "jbo", "ka", "km", "ko", "ky", "lo", "ms", "sah", "su", "th", "tt", "ug", "vi", "wo", "zh"],
            nr: [1],
            fc: 3
        }, {
            lngs: ["be", "bs", "cnr", "dz", "hr", "ru", "sr", "uk"],
            nr: [1, 2, 5],
            fc: 4
        }, {
            lngs: ["ar"],
            nr: [0, 1, 2, 3, 11, 100],
            fc: 5
        }, {
            lngs: ["cs", "sk"],
            nr: [1, 2, 5],
            fc: 6
        }, {
            lngs: ["csb", "pl"],
            nr: [1, 2, 5],
            fc: 7
        }, {
            lngs: ["cy"],
            nr: [1, 2, 3, 8],
            fc: 8
        }, {
            lngs: ["fr"],
            nr: [1, 2],
            fc: 9
        }, {
            lngs: ["ga"],
            nr: [1, 2, 3, 7, 11],
            fc: 10
        }, {
            lngs: ["gd"],
            nr: [1, 2, 3, 20],
            fc: 11
        }, {
            lngs: ["is"],
            nr: [1, 2],
            fc: 12
        }, {
            lngs: ["jv"],
            nr: [0, 1],
            fc: 13
        }, {
            lngs: ["kw"],
            nr: [1, 2, 3, 4],
            fc: 14
        }, {
            lngs: ["lt"],
            nr: [1, 2, 10],
            fc: 15
        }, {
            lngs: ["lv"],
            nr: [1, 2, 0],
            fc: 16
        }, {
            lngs: ["mk"],
            nr: [1, 2],
            fc: 17
        }, {
            lngs: ["mnk"],
            nr: [0, 1, 2],
            fc: 18
        }, {
            lngs: ["mt"],
            nr: [1, 2, 11, 20],
            fc: 19
        }, {
            lngs: ["or"],
            nr: [2, 1],
            fc: 2
        }, {
            lngs: ["ro"],
            nr: [1, 2, 20],
            fc: 20
        }, {
            lngs: ["sl"],
            nr: [5, 1, 2, 3],
            fc: 21
        }, {
            lngs: ["he", "iw"],
            nr: [1, 2, 20, 21],
            fc: 22
        }]
          , R = {
            1: function(e) {
                return Number(e > 1)
            },
            2: function(e) {
                return Number(1 != e)
            },
            3: function(e) {
                return 0
            },
            4: function(e) {
                return Number(e % 10 == 1 && e % 100 != 11 ? 0 : e % 10 >= 2 && e % 10 <= 4 && (e % 100 < 10 || e % 100 >= 20) ? 1 : 2)
            },
            5: function(e) {
                return Number(0 == e ? 0 : 1 == e ? 1 : 2 == e ? 2 : e % 100 >= 3 && e % 100 <= 10 ? 3 : e % 100 >= 11 ? 4 : 5)
            },
            6: function(e) {
                return Number(1 == e ? 0 : e >= 2 && e <= 4 ? 1 : 2)
            },
            7: function(e) {
                return Number(1 == e ? 0 : e % 10 >= 2 && e % 10 <= 4 && (e % 100 < 10 || e % 100 >= 20) ? 1 : 2)
            },
            8: function(e) {
                return Number(1 == e ? 0 : 2 == e ? 1 : 8 != e && 11 != e ? 2 : 3)
            },
            9: function(e) {
                return Number(e >= 2)
            },
            10: function(e) {
                return Number(1 == e ? 0 : 2 == e ? 1 : e < 7 ? 2 : e < 11 ? 3 : 4)
            },
            11: function(e) {
                return Number(1 == e || 11 == e ? 0 : 2 == e || 12 == e ? 1 : e > 2 && e < 20 ? 2 : 3)
            },
            12: function(e) {
                return Number(e % 10 != 1 || e % 100 == 11)
            },
            13: function(e) {
                return Number(0 !== e)
            },
            14: function(e) {
                return Number(1 == e ? 0 : 2 == e ? 1 : 3 == e ? 2 : 3)
            },
            15: function(e) {
                return Number(e % 10 == 1 && e % 100 != 11 ? 0 : e % 10 >= 2 && (e % 100 < 10 || e % 100 >= 20) ? 1 : 2)
            },
            16: function(e) {
                return Number(e % 10 == 1 && e % 100 != 11 ? 0 : 0 !== e ? 1 : 2)
            },
            17: function(e) {
                return Number(1 == e || e % 10 == 1 && e % 100 != 11 ? 0 : 1)
            },
            18: function(e) {
                return Number(0 == e ? 0 : 1 == e ? 1 : 2)
            },
            19: function(e) {
                return Number(1 == e ? 0 : 0 == e || e % 100 > 1 && e % 100 < 11 ? 1 : e % 100 > 10 && e % 100 < 20 ? 2 : 3)
            },
            20: function(e) {
                return Number(1 == e ? 0 : 0 == e || e % 100 > 0 && e % 100 < 20 ? 1 : 2)
            },
            21: function(e) {
                return Number(e % 100 == 1 ? 1 : e % 100 == 2 ? 2 : e % 100 == 3 || e % 100 == 4 ? 3 : 0)
            },
            22: function(e) {
                return Number(1 == e ? 0 : 2 == e ? 1 : (e < 0 || e > 10) && e % 10 == 0 ? 2 : 3)
            }
        }
          , D = ["v1", "v2", "v3"]
          , O = ["v4"]
          , N = {
            zero: 0,
            one: 1,
            two: 2,
            few: 3,
            many: 4,
            other: 5
        };
        class C {
            constructor(e) {
                let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : {};
                this.languageUtils = e,
                this.options = t,
                this.logger = a.create("pluralResolver"),
                (!this.options.compatibilityJSON || O.includes(this.options.compatibilityJSON)) && ("undefined" == typeof Intl || !Intl.PluralRules) && (this.options.compatibilityJSON = "v3",
                this.logger.error("Your environment seems not to be Intl API compatible, use an Intl.PluralRules polyfill. Will fallback to the compatibilityJSON v3 format handling.")),
                this.rules = function() {
                    let e = {};
                    return k.forEach(t=>{
                        t.lngs.forEach(n=>{
                            e[n] = {
                                numbers: t.nr,
                                plurals: R[t.fc]
                            }
                        }
                        )
                    }
                    ),
                    e
                }()
            }
            addRule(e, t) {
                this.rules[e] = t
            }
            getRule(e) {
                let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : {};
                if (this.shouldUseIntlApi())
                    try {
                        return new Intl.PluralRules(v(e),{
                            type: t.ordinal ? "ordinal" : "cardinal"
                        })
                    } catch {
                        return
                    }
                return this.rules[e] || this.rules[this.languageUtils.getLanguagePartFromCode(e)]
            }
            needsPlural(e) {
                let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : {}
                  , n = this.getRule(e, t);
                return this.shouldUseIntlApi() ? n && n.resolvedOptions().pluralCategories.length > 1 : n && n.numbers.length > 1
            }
            getPluralFormsOfKey(e, t) {
                let n = arguments.length > 2 && void 0 !== arguments[2] ? arguments[2] : {};
                return this.getSuffixes(e, n).map(e=>`${t}${e}`)
            }
            getSuffixes(e) {
                let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : {}
                  , n = this.getRule(e, t);
                return n ? this.shouldUseIntlApi() ? n.resolvedOptions().pluralCategories.sort((e,t)=>N[e] - N[t]).map(e=>`${this.options.prepend}${t.ordinal ? `ordinal ${this.options.prepend}` : ""}${e}`) : n.numbers.map(n=>this.getSuffix(e, n, t)) : []
            }
            getSuffix(e, t) {
                let n = arguments.length > 2 && void 0 !== arguments[2] ? arguments[2] : {}
                  , r = this.getRule(e, n);
                return r ? this.shouldUseIntlApi() ? `${this.options.prepend}${n.ordinal ? `ordinal ${this.options.prepend}` : ""}${r.select(t)}` : this.getSuffixRetroCompatible(r, t) : (this.logger.warn(`no plural rule found for: ${e}`),
                "")
            }
            getSuffixRetroCompatible(e, t) {
                let n = e.noAbs ? e.plurals(t) : e.plurals(Math.abs(t))
                  , r = e.numbers[n];
                this.options.simplifyPluralSuffix && 2 === e.numbers.length && 1 === e.numbers[0] && (2 === r ? r = "plural" : 1 === r && (r = ""));
                let i = ()=>this.options.prepend && r.toString() ? this.options.prepend + r.toString() : r.toString();
                return "v1" === this.options.compatibilityJSON ? 1 === r ? "" : "number" == typeof r ? `_plural_ ${r.toString()}` : i() : "v2" === this.options.compatibilityJSON || this.options.simplifyPluralSuffix && 2 === e.numbers.length && 1 === e.numbers[0] ? i() : this.options.prepend && n.toString() ? this.options.prepend + n.toString() : n.toString()
            }
            shouldUseIntlApi() {
                return !D.includes(this.options.compatibilityJSON)
            }
        }
        function $(e, t, n) {
            let r = arguments.length > 3 && void 0 !== arguments[3] ? arguments[3] : "."
              , i = !(arguments.length > 4) || void 0 === arguments[4] || arguments[4]
              , o = function(e, t, n) {
                let r = h(e, n);
                return void 0 !== r ? r : h(t, n)
            }(e, t, n);
            return !o && i && "string" == typeof n && void 0 === (o = y(e, n, r)) && (o = y(t, n, r)),
            o
        }
        class I {
            constructor() {
                let e = arguments.length > 0 && void 0 !== arguments[0] ? arguments[0] : {};
                this.logger = a.create("interpolator"),
                this.options = e,
                this.format = e.interpolation && e.interpolation.format || (e=>e),
                this.init(e)
            }
            init() {
                let e = arguments.length > 0 && void 0 !== arguments[0] ? arguments[0] : {};
                e.interpolation || (e.interpolation = {
                    escapeValue: !0
                });
                let t = e.interpolation;
                this.escape = void 0 !== t.escape ? t.escape : m,
                this.escapeValue = void 0 === t.escapeValue || t.escapeValue,
                this.useRawValueToEscape = void 0 !== t.useRawValueToEscape && t.useRawValueToEscape,
                this.prefix = t.prefix ? f(t.prefix) : t.prefixEscaped || "{{",
                this.suffix = t.suffix ? f(t.suffix) : t.suffixEscaped || "}}",
                this.formatSeparator = t.formatSeparator ? t.formatSeparator : t.formatSeparator || ",",
                this.unescapePrefix = t.unescapeSuffix ? "" : t.unescapePrefix || "-",
                this.unescapeSuffix = this.unescapePrefix ? "" : t.unescapeSuffix || "",
                this.nestingPrefix = t.nestingPrefix ? f(t.nestingPrefix) : t.nestingPrefixEscaped || f("$t("),
                this.nestingSuffix = t.nestingSuffix ? f(t.nestingSuffix) : t.nestingSuffixEscaped || f(")"),
                this.nestingOptionsSeparator = t.nestingOptionsSeparator ? t.nestingOptionsSeparator : t.nestingOptionsSeparator || ",",
                this.maxReplaces = t.maxReplaces ? t.maxReplaces : 1e3,
                this.alwaysFormat = void 0 !== t.alwaysFormat && t.alwaysFormat,
                this.resetRegExp()
            }
            reset() {
                this.options && this.init(this.options)
            }
            resetRegExp() {
                let e = `${this.prefix}(.+?)${this.suffix}`;
                this.regexp = RegExp(e, "g");
                let t = `${this.prefix}${this.unescapePrefix}(.+?)${this.unescapeSuffix}${this.suffix}`;
                this.regexpUnescape = RegExp(t, "g");
                let n = `${this.nestingPrefix}(.+?)${this.nestingSuffix}`;
                this.nestingRegexp = RegExp(n, "g")
            }
            interpolate(e, t, n, r) {
                let i, o, s;
                let a = this.options && this.options.interpolation && this.options.interpolation.defaultVariables || {};
                function l(e) {
                    return e.replace(/\$/g, "$$$$")
                }
                let u = e=>{
                    if (0 > e.indexOf(this.formatSeparator)) {
                        let i = $(t, a, e, this.options.keySeparator, this.options.ignoreJSONStructure);
                        return this.alwaysFormat ? this.format(i, void 0, n, {
                            ...r,
                            ...t,
                            interpolationkey: e
                        }) : i
                    }
                    let o = e.split(this.formatSeparator)
                      , s = o.shift().trim()
                      , l = o.join(this.formatSeparator).trim();
                    return this.format($(t, a, s, this.options.keySeparator, this.options.ignoreJSONStructure), l, n, {
                        ...r,
                        ...t,
                        interpolationkey: s
                    })
                }
                ;
                this.resetRegExp();
                let d = r && r.missingInterpolationHandler || this.options.missingInterpolationHandler
                  , p = r && r.interpolation && void 0 !== r.interpolation.skipOnVariables ? r.interpolation.skipOnVariables : this.options.interpolation.skipOnVariables
                  , h = [{
                    regex: this.regexpUnescape,
                    safeValue: e=>l(e)
                }, {
                    regex: this.regexp,
                    safeValue: e=>this.escapeValue ? l(this.escape(e)) : l(e)
                }];
                return h.forEach(t=>{
                    for (s = 0; i = t.regex.exec(e); ) {
                        let n = i[1].trim();
                        if (void 0 === (o = u(n))) {
                            if ("function" == typeof d) {
                                let a = d(e, i, r);
                                o = "string" == typeof a ? a : ""
                            } else if (r && Object.prototype.hasOwnProperty.call(r, n))
                                o = "";
                            else if (p) {
                                o = i[0];
                                continue
                            } else
                                this.logger.warn(`missed to pass in variable ${n} for interpolating ${e}`),
                                o = ""
                        } else
                            "string" == typeof o || this.useRawValueToEscape || (o = c(o));
                        let l = t.safeValue(o);
                        if (e = e.replace(i[0], l),
                        p ? (t.regex.lastIndex += o.length,
                        t.regex.lastIndex -= i[0].length) : t.regex.lastIndex = 0,
                        ++s >= this.maxReplaces)
                            break
                    }
                }
                ),
                e
            }
            nest(e, t) {
                let n, r, i, o = arguments.length > 2 && void 0 !== arguments[2] ? arguments[2] : {};
                function s(e, t) {
                    let n = this.nestingOptionsSeparator;
                    if (0 > e.indexOf(n))
                        return e;
                    let r = e.split(RegExp(`${n}[ ]*{`))
                      , o = `{${r[1]}`;
                    e = r[0],
                    o = this.interpolate(o, i);
                    let s = o.match(/'/g)
                      , a = o.match(/"/g);
                    (s && s.length % 2 == 0 && !a || a.length % 2 != 0) && (o = o.replace(/'/g, '"'));
                    try {
                        i = JSON.parse(o),
                        t && (i = {
                            ...t,
                            ...i
                        })
                    } catch (l) {
                        return this.logger.warn(`failed parsing options string in nesting for key ${e}`, l),
                        `${e}${n}${o}`
                    }
                    return delete i.defaultValue,
                    e
                }
                for (; n = this.nestingRegexp.exec(e); ) {
                    let a = [];
                    (i = (i = {
                        ...o
                    }).replace && "string" != typeof i.replace ? i.replace : i).applyPostProcessor = !1,
                    delete i.defaultValue;
                    let l = !1;
                    if (-1 !== n[0].indexOf(this.formatSeparator) && !/{.*}/.test(n[1])) {
                        let u = n[1].split(this.formatSeparator).map(e=>e.trim());
                        n[1] = u.shift(),
                        a = u,
                        l = !0
                    }
                    if ((r = t(s.call(this, n[1].trim(), i), i)) && n[0] === e && "string" != typeof r)
                        return r;
                    "string" != typeof r && (r = c(r)),
                    r || (this.logger.warn(`missed to resolve ${n[1]} for nesting ${e}`),
                    r = ""),
                    l && (r = a.reduce((e,t)=>this.format(e, t, o.lng, {
                        ...o,
                        interpolationkey: n[1].trim()
                    }), r.trim())),
                    e = e.replace(n[0], r),
                    this.regexp.lastIndex = 0
                }
                return e
            }
        }
        function P(e) {
            let t = {};
            return function(n, r, i) {
                let o = r + JSON.stringify(i)
                  , s = t[o];
                return s || (s = e(v(r), i),
                t[o] = s),
                s(n)
            }
        }
        class A {
            constructor() {
                let e = arguments.length > 0 && void 0 !== arguments[0] ? arguments[0] : {};
                this.logger = a.create("formatter"),
                this.options = e,
                this.formats = {
                    number: P((e,t)=>{
                        let n = new Intl.NumberFormat(e,{
                            ...t
                        });
                        return e=>n.format(e)
                    }
                    ),
                    currency: P((e,t)=>{
                        let n = new Intl.NumberFormat(e,{
                            ...t,
                            style: "currency"
                        });
                        return e=>n.format(e)
                    }
                    ),
                    datetime: P((e,t)=>{
                        let n = new Intl.DateTimeFormat(e,{
                            ...t
                        });
                        return e=>n.format(e)
                    }
                    ),
                    relativetime: P((e,t)=>{
                        let n = new Intl.RelativeTimeFormat(e,{
                            ...t
                        });
                        return e=>n.format(e, t.range || "day")
                    }
                    ),
                    list: P((e,t)=>{
                        let n = new Intl.ListFormat(e,{
                            ...t
                        });
                        return e=>n.format(e)
                    }
                    )
                },
                this.init(e)
            }
            init(e) {
                let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : {
                    interpolation: {}
                }
                  , n = t.interpolation;
                this.formatSeparator = n.formatSeparator ? n.formatSeparator : n.formatSeparator || ","
            }
            add(e, t) {
                this.formats[e.toLowerCase().trim()] = t
            }
            addCached(e, t) {
                this.formats[e.toLowerCase().trim()] = P(t)
            }
            format(e, t, n) {
                let r = arguments.length > 3 && void 0 !== arguments[3] ? arguments[3] : {}
                  , i = t.split(this.formatSeparator)
                  , o = i.reduce((e,t)=>{
                    let {formatName: i, formatOptions: o} = function(e) {
                        let t = e.toLowerCase().trim()
                          , n = {};
                        if (e.indexOf("(") > -1) {
                            let r = e.split("(");
                            t = r[0].toLowerCase().trim();
                            let i = r[1].substring(0, r[1].length - 1);
                            if ("currency" === t && 0 > i.indexOf(":"))
                                n.currency || (n.currency = i.trim());
                            else if ("relativetime" === t && 0 > i.indexOf(":"))
                                n.range || (n.range = i.trim());
                            else {
                                let o = i.split(";");
                                o.forEach(e=>{
                                    if (!e)
                                        return;
                                    let[t,...r] = e.split(":")
                                      , i = r.join(":").trim().replace(/^'+|'+$/g, "");
                                    n[t.trim()] || (n[t.trim()] = i),
                                    "false" === i && (n[t.trim()] = !1),
                                    "true" === i && (n[t.trim()] = !0),
                                    isNaN(i) || (n[t.trim()] = parseInt(i, 10))
                                }
                                )
                            }
                        }
                        return {
                            formatName: t,
                            formatOptions: n
                        }
                    }(t);
                    if (this.formats[i]) {
                        let s = e;
                        try {
                            let a = r && r.formatParams && r.formatParams[r.interpolationkey] || {}
                              , l = a.locale || a.lng || r.locale || r.lng || n;
                            s = this.formats[i](e, l, {
                                ...o,
                                ...r,
                                ...a
                            })
                        } catch (u) {
                            this.logger.warn(u)
                        }
                        return s
                    }
                    return this.logger.warn(`there was no format function for ${i}`),
                    e
                }
                , e);
                return o
            }
        }
        class L extends l {
            constructor(e, t, n) {
                let r = arguments.length > 3 && void 0 !== arguments[3] ? arguments[3] : {};
                super(),
                this.backend = e,
                this.store = t,
                this.services = n,
                this.languageUtils = n.languageUtils,
                this.options = r,
                this.logger = a.create("backendConnector"),
                this.waitingReads = [],
                this.maxParallelReads = r.maxParallelReads || 10,
                this.readingCalls = 0,
                this.maxRetries = r.maxRetries >= 0 ? r.maxRetries : 5,
                this.retryTimeout = r.retryTimeout >= 1 ? r.retryTimeout : 350,
                this.state = {},
                this.queue = [],
                this.backend && this.backend.init && this.backend.init(n, r.backend, r)
            }
            queueLoad(e, t, n, r) {
                let i = {}
                  , o = {}
                  , s = {}
                  , a = {};
                return e.forEach(e=>{
                    let r = !0;
                    t.forEach(t=>{
                        let s = `${e}|${t}`;
                        !n.reload && this.store.hasResourceBundle(e, t) ? this.state[s] = 2 : this.state[s] < 0 || (1 === this.state[s] ? void 0 === o[s] && (o[s] = !0) : (this.state[s] = 1,
                        r = !1,
                        void 0 === o[s] && (o[s] = !0),
                        void 0 === i[s] && (i[s] = !0),
                        void 0 === a[t] && (a[t] = !0)))
                    }
                    ),
                    r || (s[e] = !0)
                }
                ),
                (Object.keys(i).length || Object.keys(o).length) && this.queue.push({
                    pending: o,
                    pendingCount: Object.keys(o).length,
                    loaded: {},
                    errors: [],
                    callback: r
                }),
                {
                    toLoad: Object.keys(i),
                    pending: Object.keys(o),
                    toLoadLanguages: Object.keys(s),
                    toLoadNamespaces: Object.keys(a)
                }
            }
            loaded(e, t, n) {
                let r = e.split("|")
                  , i = r[0]
                  , o = r[1];
                t && this.emit("failedLoading", i, o, t),
                n && this.store.addResourceBundle(i, o, n),
                this.state[e] = t ? -1 : 2;
                let s = {};
                this.queue.forEach(n=>{
                    var r;
                    (function(e, t, n, r) {
                        let {obj: i, k: o} = d(e, t, Object);
                        i[o] = i[o] || [],
                        r && (i[o] = i[o].concat(n)),
                        r || i[o].push(n)
                    }
                    )(n.loaded, [i], o),
                    void 0 !== (r = n).pending[e] && (delete r.pending[e],
                    r.pendingCount--),
                    t && n.errors.push(t),
                    0 !== n.pendingCount || n.done || (Object.keys(n.loaded).forEach(e=>{
                        s[e] || (s[e] = {});
                        let t = n.loaded[e];
                        t.length && t.forEach(t=>{
                            void 0 === s[e][t] && (s[e][t] = !0)
                        }
                        )
                    }
                    ),
                    n.done = !0,
                    n.errors.length ? n.callback(n.errors) : n.callback())
                }
                ),
                this.emit("loaded", s),
                this.queue = this.queue.filter(e=>!e.done)
            }
            read(e, t, n) {
                let r = arguments.length > 3 && void 0 !== arguments[3] ? arguments[3] : 0
                  , i = arguments.length > 4 && void 0 !== arguments[4] ? arguments[4] : this.retryTimeout
                  , o = arguments.length > 5 ? arguments[5] : void 0;
                if (!e.length)
                    return o(null, {});
                if (this.readingCalls >= this.maxParallelReads) {
                    this.waitingReads.push({
                        lng: e,
                        ns: t,
                        fcName: n,
                        tried: r,
                        wait: i,
                        callback: o
                    });
                    return
                }
                this.readingCalls++;
                let s = (s,a)=>{
                    if (this.readingCalls--,
                    this.waitingReads.length > 0) {
                        let l = this.waitingReads.shift();
                        this.read(l.lng, l.ns, l.fcName, l.tried, l.wait, l.callback)
                    }
                    if (s && a && r < this.maxRetries) {
                        setTimeout(()=>{
                            this.read.call(this, e, t, n, r + 1, 2 * i, o)
                        }
                        , i);
                        return
                    }
                    o(s, a)
                }
                  , a = this.backend[n].bind(this.backend);
                if (2 === a.length) {
                    try {
                        let l = a(e, t);
                        l && "function" == typeof l.then ? l.then(e=>s(null, e)).catch(s) : s(null, l)
                    } catch (u) {
                        s(u)
                    }
                    return
                }
                return a(e, t, s)
            }
            prepareLoading(e, t) {
                let n = arguments.length > 2 && void 0 !== arguments[2] ? arguments[2] : {}
                  , r = arguments.length > 3 ? arguments[3] : void 0;
                if (!this.backend)
                    return this.logger.warn("No backend was added via i18next.use. Will not load resources."),
                    r && r();
                "string" == typeof e && (e = this.languageUtils.toResolveHierarchy(e)),
                "string" == typeof t && (t = [t]);
                let i = this.queueLoad(e, t, n, r);
                if (!i.toLoad.length)
                    return i.pending.length || r(),
                    null;
                i.toLoad.forEach(e=>{
                    this.loadOne(e)
                }
                )
            }
            load(e, t, n) {
                this.prepareLoading(e, t, {}, n)
            }
            reload(e, t, n) {
                this.prepareLoading(e, t, {
                    reload: !0
                }, n)
            }
            loadOne(e) {
                let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : ""
                  , n = e.split("|")
                  , r = n[0]
                  , i = n[1];
                this.read(r, i, "read", void 0, void 0, (n,o)=>{
                    n && this.logger.warn(`${t}loading namespace ${i} for language ${r} failed`, n),
                    !n && o && this.logger.log(`${t}loaded namespace ${i} for language ${r}`, o),
                    this.loaded(e, n, o)
                }
                )
            }
            saveMissing(e, t, n, r, i) {
                let o = arguments.length > 5 && void 0 !== arguments[5] ? arguments[5] : {}
                  , s = arguments.length > 6 && void 0 !== arguments[6] ? arguments[6] : ()=>{}
                ;
                if (this.services.utils && this.services.utils.hasLoadedNamespace && !this.services.utils.hasLoadedNamespace(t)) {
                    this.logger.warn(`did not save key "${n}" as the namespace "${t}" was not yet loaded`, "This means something IS WRONG in your setup. You access the t function before i18next.init / i18next.loadNamespace / i18next.changeLanguage was done. Wait for the callback or Promise to resolve before accessing it!!!");
                    return
                }
                if (null != n && "" !== n) {
                    if (this.backend && this.backend.create) {
                        let a = {
                            ...o,
                            isUpdate: i
                        }
                          , l = this.backend.create.bind(this.backend);
                        if (l.length < 6)
                            try {
                                let u;
                                (u = 5 === l.length ? l(e, t, n, r, a) : l(e, t, n, r)) && "function" == typeof u.then ? u.then(e=>s(null, e)).catch(s) : s(null, u)
                            } catch (c) {
                                s(c)
                            }
                        else
                            l(e, t, n, r, s, a)
                    }
                    e && e[0] && this.store.addResource(e[0], t, n, r)
                }
            }
        }
        function U() {
            return {
                debug: !1,
                initImmediate: !0,
                ns: ["translation"],
                defaultNS: ["translation"],
                fallbackLng: ["dev"],
                fallbackNS: !1,
                supportedLngs: !1,
                nonExplicitSupportedLngs: !1,
                load: "all",
                preload: !1,
                simplifyPluralSuffix: !0,
                keySeparator: ".",
                nsSeparator: ":",
                pluralSeparator: "_",
                contextSeparator: "_",
                partialBundledLanguages: !1,
                saveMissing: !1,
                updateMissing: !1,
                saveMissingTo: "fallback",
                saveMissingPlurals: !0,
                missingKeyHandler: !1,
                missingInterpolationHandler: !1,
                postProcess: !1,
                postProcessPassResolved: !1,
                returnNull: !1,
                returnEmptyString: !0,
                returnObjects: !1,
                joinArrays: !1,
                returnedObjectHandler: !1,
                parseMissingKeyHandler: !1,
                appendNamespaceToMissingKey: !1,
                appendNamespaceToCIMode: !1,
                overloadTranslationOptionHandler: function(e) {
                    let t = {};
                    if ("object" == typeof e[1] && (t = e[1]),
                    "string" == typeof e[1] && (t.defaultValue = e[1]),
                    "string" == typeof e[2] && (t.tDescription = e[2]),
                    "object" == typeof e[2] || "object" == typeof e[3]) {
                        let n = e[3] || e[2];
                        Object.keys(n).forEach(e=>{
                            t[e] = n[e]
                        }
                        )
                    }
                    return t
                },
                interpolation: {
                    escapeValue: !0,
                    format: (e,t,n,r)=>e,
                    prefix: "{{",
                    suffix: "}}",
                    formatSeparator: ",",
                    unescapePrefix: "-",
                    nestingPrefix: "$t(",
                    nestingSuffix: ")",
                    nestingOptionsSeparator: ",",
                    maxReplaces: 1e3,
                    skipOnVariables: !0
                }
            }
        }
        function j(e) {
            return "string" == typeof e.ns && (e.ns = [e.ns]),
            "string" == typeof e.fallbackLng && (e.fallbackLng = [e.fallbackLng]),
            "string" == typeof e.fallbackNS && (e.fallbackNS = [e.fallbackNS]),
            e.supportedLngs && 0 > e.supportedLngs.indexOf("cimode") && (e.supportedLngs = e.supportedLngs.concat(["cimode"])),
            e
        }
        function B() {}
        class Y extends l {
            constructor() {
                let e = arguments.length > 0 && void 0 !== arguments[0] ? arguments[0] : {}
                  , t = arguments.length > 1 ? arguments[1] : void 0;
                if (super(),
                this.options = j(e),
                this.services = {},
                this.logger = a,
                this.modules = {
                    external: []
                },
                !function(e) {
                    let t = Object.getOwnPropertyNames(Object.getPrototypeOf(e));
                    t.forEach(t=>{
                        "function" == typeof e[t] && (e[t] = e[t].bind(e))
                    }
                    )
                }(this),
                t && !this.isInitialized && !e.isClone) {
                    if (!this.options.initImmediate)
                        return this.init(e, t),
                        this;
                    setTimeout(()=>{
                        this.init(e, t)
                    }
                    , 0)
                }
            }
            init() {
                var e = this;
                let t = arguments.length > 0 && void 0 !== arguments[0] ? arguments[0] : {}
                  , n = arguments.length > 1 ? arguments[1] : void 0;
                "function" == typeof t && (n = t,
                t = {}),
                !t.defaultNS && !1 !== t.defaultNS && t.ns && ("string" == typeof t.ns ? t.defaultNS = t.ns : 0 > t.ns.indexOf("translation") && (t.defaultNS = t.ns[0]));
                let r = U();
                function i(e) {
                    return e ? "function" == typeof e ? new e : e : null
                }
                if (this.options = {
                    ...r,
                    ...this.options,
                    ...j(t)
                },
                "v1" !== this.options.compatibilityAPI && (this.options.interpolation = {
                    ...r.interpolation,
                    ...this.options.interpolation
                }),
                void 0 !== t.keySeparator && (this.options.userDefinedKeySeparator = t.keySeparator),
                void 0 !== t.nsSeparator && (this.options.userDefinedNsSeparator = t.nsSeparator),
                !this.options.isClone) {
                    let o;
                    this.modules.logger ? a.init(i(this.modules.logger), this.options) : a.init(null, this.options),
                    this.modules.formatter ? o = this.modules.formatter : "undefined" != typeof Intl && (o = A);
                    let s = new T(this.options);
                    this.store = new b(this.options.resources,this.options);
                    let l = this.services;
                    l.logger = a,
                    l.resourceStore = this.store,
                    l.languageUtils = s,
                    l.pluralResolver = new C(s,{
                        prepend: this.options.pluralSeparator,
                        compatibilityJSON: this.options.compatibilityJSON,
                        simplifyPluralSuffix: this.options.simplifyPluralSuffix
                    }),
                    o && (!this.options.interpolation.format || this.options.interpolation.format === r.interpolation.format) && (l.formatter = i(o),
                    l.formatter.init(l, this.options),
                    this.options.interpolation.format = l.formatter.format.bind(l.formatter)),
                    l.interpolator = new I(this.options),
                    l.utils = {
                        hasLoadedNamespace: this.hasLoadedNamespace.bind(this)
                    },
                    l.backendConnector = new L(i(this.modules.backend),l.resourceStore,l,this.options),
                    l.backendConnector.on("*", function(t) {
                        for (var n = arguments.length, r = Array(n > 1 ? n - 1 : 0), i = 1; i < n; i++)
                            r[i - 1] = arguments[i];
                        e.emit(t, ...r)
                    }),
                    this.modules.languageDetector && (l.languageDetector = i(this.modules.languageDetector),
                    l.languageDetector.init && l.languageDetector.init(l, this.options.detection, this.options)),
                    this.modules.i18nFormat && (l.i18nFormat = i(this.modules.i18nFormat),
                    l.i18nFormat.init && l.i18nFormat.init(this)),
                    this.translator = new w(this.services,this.options),
                    this.translator.on("*", function(t) {
                        for (var n = arguments.length, r = Array(n > 1 ? n - 1 : 0), i = 1; i < n; i++)
                            r[i - 1] = arguments[i];
                        e.emit(t, ...r)
                    }),
                    this.modules.external.forEach(e=>{
                        e.init && e.init(this)
                    }
                    )
                }
                if (this.format = this.options.interpolation.format,
                n || (n = B),
                this.options.fallbackLng && !this.services.languageDetector && !this.options.lng) {
                    let c = this.services.languageUtils.getFallbackCodes(this.options.fallbackLng);
                    c.length > 0 && "dev" !== c[0] && (this.options.lng = c[0])
                }
                this.services.languageDetector || this.options.lng || this.logger.warn("init: no languageDetector is used and no lng is defined"),
                ["getResource", "hasResourceBundle", "getResourceBundle", "getDataByLanguage"].forEach(t=>{
                    this[t] = function() {
                        return e.store[t](...arguments)
                    }
                }
                ),
                ["addResource", "addResources", "addResourceBundle", "removeResourceBundle"].forEach(t=>{
                    this[t] = function() {
                        return e.store[t](...arguments),
                        e
                    }
                }
                );
                let d = u()
                  , p = ()=>{
                    let e = (e,t)=>{
                        this.isInitialized && !this.initializedStoreOnce && this.logger.warn("init: i18next is already initialized. You should call init just once!"),
                        this.isInitialized = !0,
                        this.options.isClone || this.logger.log("initialized", this.options),
                        this.emit("initialized", this.options),
                        d.resolve(t),
                        n(e, t)
                    }
                    ;
                    if (this.languages && "v1" !== this.options.compatibilityAPI && !this.isInitialized)
                        return e(null, this.t.bind(this));
                    this.changeLanguage(this.options.lng, e)
                }
                ;
                return this.options.resources || !this.options.initImmediate ? p() : setTimeout(p, 0),
                d
            }
            loadResources(e) {
                let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : B
                  , n = t
                  , r = "string" == typeof e ? e : this.language;
                if ("function" == typeof e && (n = e),
                !this.options.resources || this.options.partialBundledLanguages) {
                    if (r && "cimode" === r.toLowerCase())
                        return n();
                    let i = []
                      , o = e=>{
                        if (!e)
                            return;
                        let t = this.services.languageUtils.toResolveHierarchy(e);
                        t.forEach(e=>{
                            0 > i.indexOf(e) && i.push(e)
                        }
                        )
                    }
                    ;
                    if (r)
                        o(r);
                    else {
                        let s = this.services.languageUtils.getFallbackCodes(this.options.fallbackLng);
                        s.forEach(e=>o(e))
                    }
                    this.options.preload && this.options.preload.forEach(e=>o(e)),
                    this.services.backendConnector.load(i, this.options.ns, e=>{
                        e || this.resolvedLanguage || !this.language || this.setResolvedLanguage(this.language),
                        n(e)
                    }
                    )
                } else
                    n(null)
            }
            reloadResources(e, t, n) {
                let r = u();
                return e || (e = this.languages),
                t || (t = this.options.ns),
                n || (n = B),
                this.services.backendConnector.reload(e, t, e=>{
                    r.resolve(),
                    n(e)
                }
                ),
                r
            }
            use(e) {
                if (!e)
                    throw Error("You are passing an undefined module! Please check the object you are passing to i18next.use()");
                if (!e.type)
                    throw Error("You are passing a wrong module! Please check the object you are passing to i18next.use()");
                return "backend" === e.type && (this.modules.backend = e),
                ("logger" === e.type || e.log && e.warn && e.error) && (this.modules.logger = e),
                "languageDetector" === e.type && (this.modules.languageDetector = e),
                "i18nFormat" === e.type && (this.modules.i18nFormat = e),
                "postProcessor" === e.type && S.addPostProcessor(e),
                "formatter" === e.type && (this.modules.formatter = e),
                "3rdParty" === e.type && this.modules.external.push(e),
                this
            }
            setResolvedLanguage(e) {
                if (e && this.languages && !(["cimode", "dev"].indexOf(e) > -1))
                    for (let t = 0; t < this.languages.length; t++) {
                        let n = this.languages[t];
                        if (!(["cimode", "dev"].indexOf(n) > -1) && this.store.hasLanguageSomeTranslations(n)) {
                            this.resolvedLanguage = n;
                            break
                        }
                    }
            }
            changeLanguage(e, t) {
                var n = this;
                this.isLanguageChangingTo = e;
                let r = u();
                this.emit("languageChanging", e);
                let i = e=>{
                    this.language = e,
                    this.languages = this.services.languageUtils.toResolveHierarchy(e),
                    this.resolvedLanguage = void 0,
                    this.setResolvedLanguage(e)
                }
                  , o = (e,o)=>{
                    o ? (i(o),
                    this.translator.changeLanguage(o),
                    this.isLanguageChangingTo = void 0,
                    this.emit("languageChanged", o),
                    this.logger.log("languageChanged", o)) : this.isLanguageChangingTo = void 0,
                    r.resolve(function() {
                        return n.t(...arguments)
                    }),
                    t && t(e, function() {
                        return n.t(...arguments)
                    })
                }
                  , s = t=>{
                    e || t || !this.services.languageDetector || (t = []);
                    let n = "string" == typeof t ? t : this.services.languageUtils.getBestMatchFromCodes(t);
                    n && (this.language || i(n),
                    this.translator.language || this.translator.changeLanguage(n),
                    this.services.languageDetector && this.services.languageDetector.cacheUserLanguage && this.services.languageDetector.cacheUserLanguage(n)),
                    this.loadResources(n, e=>{
                        o(e, n)
                    }
                    )
                }
                ;
                return e || !this.services.languageDetector || this.services.languageDetector.async ? !e && this.services.languageDetector && this.services.languageDetector.async ? 0 === this.services.languageDetector.detect.length ? this.services.languageDetector.detect().then(s) : this.services.languageDetector.detect(s) : s(e) : s(this.services.languageDetector.detect()),
                r
            }
            getFixedT(e, t, n) {
                var r = this;
                let i = function(e, t) {
                    let o, s;
                    if ("object" != typeof t) {
                        for (var a = arguments.length, l = Array(a > 2 ? a - 2 : 0), u = 2; u < a; u++)
                            l[u - 2] = arguments[u];
                        o = r.options.overloadTranslationOptionHandler([e, t].concat(l))
                    } else
                        o = {
                            ...t
                        };
                    o.lng = o.lng || i.lng,
                    o.lngs = o.lngs || i.lngs,
                    o.ns = o.ns || i.ns,
                    o.keyPrefix = o.keyPrefix || n || i.keyPrefix;
                    let c = r.options.keySeparator || ".";
                    return s = o.keyPrefix && Array.isArray(e) ? e.map(e=>`${o.keyPrefix}${c}${e}`) : o.keyPrefix ? `${o.keyPrefix}${c}${e}` : e,
                    r.t(s, o)
                };
                return "string" == typeof e ? i.lng = e : i.lngs = e,
                i.ns = t,
                i.keyPrefix = n,
                i
            }
            t() {
                return this.translator && this.translator.translate(...arguments)
            }
            exists() {
                return this.translator && this.translator.exists(...arguments)
            }
            setDefaultNamespace(e) {
                this.options.defaultNS = e
            }
            hasLoadedNamespace(e) {
                let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : {};
                if (!this.isInitialized)
                    return this.logger.warn("hasLoadedNamespace: i18next was not initialized", this.languages),
                    !1;
                if (!this.languages || !this.languages.length)
                    return this.logger.warn("hasLoadedNamespace: i18n.languages were undefined or empty", this.languages),
                    !1;
                let n = t.lng || this.resolvedLanguage || this.languages[0]
                  , r = !!this.options && this.options.fallbackLng
                  , i = this.languages[this.languages.length - 1];
                if ("cimode" === n.toLowerCase())
                    return !0;
                let o = (e,t)=>{
                    let n = this.services.backendConnector.state[`${e}|${t}`];
                    return -1 === n || 2 === n
                }
                ;
                if (t.precheck) {
                    let s = t.precheck(this, o);
                    if (void 0 !== s)
                        return s
                }
                return !!(this.hasResourceBundle(n, e) || !this.services.backendConnector.backend || this.options.resources && !this.options.partialBundledLanguages || o(n, e) && (!r || o(i, e)))
            }
            loadNamespaces(e, t) {
                let n = u();
                return this.options.ns ? ("string" == typeof e && (e = [e]),
                e.forEach(e=>{
                    0 > this.options.ns.indexOf(e) && this.options.ns.push(e)
                }
                ),
                this.loadResources(e=>{
                    n.resolve(),
                    t && t(e)
                }
                ),
                n) : (t && t(),
                Promise.resolve())
            }
            loadLanguages(e, t) {
                let n = u();
                "string" == typeof e && (e = [e]);
                let r = this.options.preload || []
                  , i = e.filter(e=>0 > r.indexOf(e));
                return i.length ? (this.options.preload = r.concat(i),
                this.loadResources(e=>{
                    n.resolve(),
                    t && t(e)
                }
                ),
                n) : (t && t(),
                Promise.resolve())
            }
            dir(e) {
                if (e || (e = this.resolvedLanguage || (this.languages && this.languages.length > 0 ? this.languages[0] : this.language)),
                !e)
                    return "rtl";
                let t = this.services && this.services.languageUtils || new T(U());
                return ["ar", "shu", "sqr", "ssh", "xaa", "yhd", "yud", "aao", "abh", "abv", "acm", "acq", "acw", "acx", "acy", "adf", "ads", "aeb", "aec", "afb", "ajp", "apc", "apd", "arb", "arq", "ars", "ary", "arz", "auz", "avl", "ayh", "ayl", "ayn", "ayp", "bbz", "pga", "he", "iw", "ps", "pbt", "pbu", "pst", "prp", "prd", "ug", "ur", "ydd", "yds", "yih", "ji", "yi", "hbo", "men", "xmn", "fa", "jpr", "peo", "pes", "prs", "dv", "sam", "ckb"].indexOf(t.getLanguagePartFromCode(e)) > -1 || e.toLowerCase().indexOf("-arab") > 1 ? "rtl" : "ltr"
            }
            static createInstance() {
                let e = arguments.length > 0 && void 0 !== arguments[0] ? arguments[0] : {}
                  , t = arguments.length > 1 ? arguments[1] : void 0;
                return new Y(e,t)
            }
            cloneInstance() {
                let e = arguments.length > 0 && void 0 !== arguments[0] ? arguments[0] : {}
                  , t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : B
                  , n = e.forkResourceStore;
                n && delete e.forkResourceStore;
                let r = {
                    ...this.options,
                    ...e,
                    isClone: !0
                }
                  , i = new Y(r);
                return (void 0 !== e.debug || void 0 !== e.prefix) && (i.logger = i.logger.clone(e)),
                ["store", "services", "language"].forEach(e=>{
                    i[e] = this[e]
                }
                ),
                i.services = {
                    ...this.services
                },
                i.services.utils = {
                    hasLoadedNamespace: i.hasLoadedNamespace.bind(i)
                },
                n && (i.store = new b(this.store.data,r),
                i.services.resourceStore = i.store),
                i.translator = new w(i.services,r),
                i.translator.on("*", function(e) {
                    for (var t = arguments.length, n = Array(t > 1 ? t - 1 : 0), r = 1; r < t; r++)
                        n[r - 1] = arguments[r];
                    i.emit(e, ...n)
                }),
                i.init(r, t),
                i.translator.options = r,
                i.translator.backendConnector.services.utils = {
                    hasLoadedNamespace: i.hasLoadedNamespace.bind(i)
                },
                i
            }
            toJSON() {
                return {
                    options: this.options,
                    store: this.store,
                    language: this.language,
                    languages: this.languages,
                    resolvedLanguage: this.resolvedLanguage
                }
            }
        }
        let M = Y.createInstance();
        M.createInstance = Y.createInstance,
        M.createInstance,
        M.dir,
        M.init,
        M.loadResources,
        M.reloadResources,
        M.use,
        M.changeLanguage,
        M.getFixedT,
        M.t,
        M.exists,
        M.setDefaultNamespace,
        M.hasLoadedNamespace,
        M.loadNamespaces,
        M.loadLanguages;
        var G = n(17527)
          , V = n(66979);
        let H = {
            en: {
                common: {},
                ...n(47156).Z
            },
            ja: {
                common: {},
                ...n(54399).Z
            }
        }
          , F = M.createInstance({
            defaultNS: "common",
            resources: H,
            ns: ["common", "privacyPolicyUpdate", "ogp", "footer", "studio", "topPage", "studioPage"],
            returnObjects: !0,
            interpolation: {
                escapeValue: !1
            },
            initImmediate: !0
        }).use(G.Db);
        F.init();
        let z = (e,t)=>{
            let {t: n, i18n: r, ready: i} = (0,
            G.$G)(e, t);
            return {
                t: n,
                i18n: r,
                ready: i
            }
        }
          , q = e=>{
            let {lng: t, children: n} = e
              , o = (0,
            i.useMemo)(()=>F.cloneInstance({
                lng: t
            }), [t]);
            return (0,
            V.Pf)(()=>{
                o.changeLanguage(t)
            }
            , [t]),
            (0,
            r.jsx)(G.a3, {
                i18n: o,
                children: n
            })
        }
    },
    16560: function(e, t, n) {
        "use strict";
        n.r(t),
        n.d(t, {
            default: function() {
                return eU
            }
        });
        var r, i, o, s = n(85893), a = n(67294), l = function() {
            function e() {
                this.keyToValue = new Map,
                this.valueToKey = new Map
            }
            return e.prototype.set = function(e, t) {
                this.keyToValue.set(e, t),
                this.valueToKey.set(t, e)
            }
            ,
            e.prototype.getByKey = function(e) {
                return this.keyToValue.get(e)
            }
            ,
            e.prototype.getByValue = function(e) {
                return this.valueToKey.get(e)
            }
            ,
            e.prototype.clear = function() {
                this.keyToValue.clear(),
                this.valueToKey.clear()
            }
            ,
            e
        }(), u = function() {
            function e(e) {
                this.generateIdentifier = e,
                this.kv = new l
            }
            return e.prototype.register = function(e, t) {
                this.kv.getByValue(e) || (t || (t = this.generateIdentifier(e)),
                this.kv.set(t, e))
            }
            ,
            e.prototype.clear = function() {
                this.kv.clear()
            }
            ,
            e.prototype.getIdentifier = function(e) {
                return this.kv.getByValue(e)
            }
            ,
            e.prototype.getValue = function(e) {
                return this.kv.getByKey(e)
            }
            ,
            e
        }(), c = (r = function(e, t) {
            return (r = Object.setPrototypeOf || ({
                __proto__: []
            })instanceof Array && function(e, t) {
                e.__proto__ = t
            }
            || function(e, t) {
                for (var n in t)
                    Object.prototype.hasOwnProperty.call(t, n) && (e[n] = t[n])
            }
            )(e, t)
        }
        ,
        function(e, t) {
            if ("function" != typeof t && null !== t)
                throw TypeError("Class extends value " + String(t) + " is not a constructor or null");
            function n() {
                this.constructor = e
            }
            r(e, t),
            e.prototype = null === t ? Object.create(t) : (n.prototype = t.prototype,
            new n)
        }
        ), d = function(e) {
            function t() {
                var t = e.call(this, function(e) {
                    return e.name
                }) || this;
                return t.classToAllowedProps = new Map,
                t
            }
            return c(t, e),
            t.prototype.register = function(t, n) {
                "object" == typeof n ? (n.allowProps && this.classToAllowedProps.set(t, n.allowProps),
                e.prototype.register.call(this, t, n.identifier)) : e.prototype.register.call(this, t, n)
            }
            ,
            t.prototype.getAllowedProps = function(e) {
                return this.classToAllowedProps.get(e)
            }
            ,
            t
        }(u), p = function(e, t) {
            var n = "function" == typeof Symbol && e[Symbol.iterator];
            if (!n)
                return e;
            var r, i, o = n.call(e), s = [];
            try {
                for (; (void 0 === t || t-- > 0) && !(r = o.next()).done; )
                    s.push(r.value)
            } catch (a) {
                i = {
                    error: a
                }
            } finally {
                try {
                    r && !r.done && (n = o.return) && n.call(o)
                } finally {
                    if (i)
                        throw i.error
                }
            }
            return s
        };
        function h(e, t) {
            Object.entries(e).forEach(function(e) {
                var n = p(e, 2)
                  , r = n[0];
                return t(n[1], r)
            })
        }
        function f(e, t) {
            return -1 !== e.indexOf(t)
        }
        function g(e, t) {
            for (var n = 0; n < e.length; n++) {
                var r = e[n];
                if (t(r))
                    return r
            }
        }
        var m = function() {
            function e() {
                this.transfomers = {}
            }
            return e.prototype.register = function(e) {
                this.transfomers[e.name] = e
            }
            ,
            e.prototype.findApplicable = function(e) {
                return function(e, t) {
                    var n = function(e) {
                        if ("values"in Object)
                            return Object.values(e);
                        var t = [];
                        for (var n in e)
                            e.hasOwnProperty(n) && t.push(e[n]);
                        return t
                    }(e);
                    if ("find"in n)
                        return n.find(t);
                    for (var r = 0; r < n.length; r++) {
                        var i = n[r];
                        if (t(i))
                            return i
                    }
                }(this.transfomers, function(t) {
                    return t.isApplicable(e)
                })
            }
            ,
            e.prototype.findByName = function(e) {
                return this.transfomers[e]
            }
            ,
            e
        }()
          , _ = function(e) {
            return void 0 === e
        }
          , y = function(e) {
            return "object" == typeof e && null !== e && e !== Object.prototype && (null === Object.getPrototypeOf(e) || Object.getPrototypeOf(e) === Object.prototype)
        }
          , v = function(e) {
            return y(e) && 0 === Object.keys(e).length
        }
          , b = function(e) {
            return Array.isArray(e)
        }
          , S = function(e) {
            return e instanceof Map
        }
          , E = function(e) {
            return e instanceof Set
        }
          , w = function(e) {
            return "Symbol" === Object.prototype.toString.call(e).slice(8, -1)
        }
          , x = function(e) {
            return "number" == typeof e && isNaN(e)
        }
          , T = function(e) {
            return e.replace(/\./g, "\\.")
        }
          , k = function(e) {
            return e.map(String).map(T).join(".")
        }
          , R = function(e) {
            for (var t = [], n = "", r = 0; r < e.length; r++) {
                var i = e.charAt(r);
                if ("\\" === i && "." === e.charAt(r + 1)) {
                    n += ".",
                    r++;
                    continue
                }
                if ("." === i) {
                    t.push(n),
                    n = "";
                    continue
                }
                n += i
            }
            var o = n;
            return t.push(o),
            t
        }
          , D = function() {
            return (D = Object.assign || function(e) {
                for (var t, n = 1, r = arguments.length; n < r; n++)
                    for (var i in t = arguments[n])
                        Object.prototype.hasOwnProperty.call(t, i) && (e[i] = t[i]);
                return e
            }
            ).apply(this, arguments)
        }
          , O = function(e, t) {
            var n = "function" == typeof Symbol && e[Symbol.iterator];
            if (!n)
                return e;
            var r, i, o = n.call(e), s = [];
            try {
                for (; (void 0 === t || t-- > 0) && !(r = o.next()).done; )
                    s.push(r.value)
            } catch (a) {
                i = {
                    error: a
                }
            } finally {
                try {
                    r && !r.done && (n = o.return) && n.call(o)
                } finally {
                    if (i)
                        throw i.error
                }
            }
            return s
        }
          , N = function(e, t) {
            for (var n = 0, r = t.length, i = e.length; n < r; n++,
            i++)
                e[i] = t[n];
            return e
        };
        function C(e, t, n, r) {
            return {
                isApplicable: e,
                annotation: t,
                transform: n,
                untransform: r
            }
        }
        var $ = [C(_, "undefined", function() {
            return null
        }, function() {}), C(function(e) {
            return "bigint" == typeof e
        }, "bigint", function(e) {
            return e.toString()
        }, function(e) {
            return "undefined" != typeof BigInt ? BigInt(e) : (console.error("Please add a BigInt polyfill."),
            e)
        }), C(function(e) {
            return e instanceof Date && !isNaN(e.valueOf())
        }, "Date", function(e) {
            return e.toISOString()
        }, function(e) {
            return new Date(e)
        }), C(function(e) {
            return e instanceof Error
        }, "Error", function(e, t) {
            var n = {
                name: e.name,
                message: e.message
            };
            return t.allowedErrorProps.forEach(function(t) {
                n[t] = e[t]
            }),
            n
        }, function(e, t) {
            var n = Error(e.message);
            return n.name = e.name,
            n.stack = e.stack,
            t.allowedErrorProps.forEach(function(t) {
                n[t] = e[t]
            }),
            n
        }), C(function(e) {
            return e instanceof RegExp
        }, "regexp", function(e) {
            return "" + e
        }, function(e) {
            return RegExp(e.slice(1, e.lastIndexOf("/")), e.slice(e.lastIndexOf("/") + 1))
        }), C(E, "set", function(e) {
            return N([], O(e.values()))
        }, function(e) {
            return new Set(e)
        }), C(S, "map", function(e) {
            return N([], O(e.entries()))
        }, function(e) {
            return new Map(e)
        }), C(function(e) {
            var t;
            return x(e) || (t = e) === 1 / 0 || t === -1 / 0
        }, "number", function(e) {
            return x(e) ? "NaN" : e > 0 ? "Infinity" : "-Infinity"
        }, Number), C(function(e) {
            return 0 === e && 1 / e == -1 / 0
        }, "number", function() {
            return "-0"
        }, Number), C(function(e) {
            return e instanceof URL
        }, "URL", function(e) {
            return e.toString()
        }, function(e) {
            return new URL(e)
        })];
        function I(e, t, n, r) {
            return {
                isApplicable: e,
                annotation: t,
                transform: n,
                untransform: r
            }
        }
        var P = I(function(e, t) {
            return !!w(e) && !!t.symbolRegistry.getIdentifier(e)
        }, function(e, t) {
            return ["symbol", t.symbolRegistry.getIdentifier(e)]
        }, function(e) {
            return e.description
        }, function(e, t, n) {
            var r = n.symbolRegistry.getValue(t[1]);
            if (!r)
                throw Error("Trying to deserialize unknown symbol");
            return r
        })
          , A = [Int8Array, Uint8Array, Int16Array, Uint16Array, Int32Array, Uint32Array, Float32Array, Float64Array, Uint8ClampedArray].reduce(function(e, t) {
            return e[t.name] = t,
            e
        }, {})
          , L = I(function(e) {
            return ArrayBuffer.isView(e) && !(e instanceof DataView)
        }, function(e) {
            return ["typed-array", e.constructor.name]
        }, function(e) {
            return N([], O(e))
        }, function(e, t) {
            var n = A[t[1]];
            if (!n)
                throw Error("Trying to deserialize unknown typed array");
            return new n(e)
        });
        function U(e, t) {
            return null != e && !!e.constructor && !!t.classRegistry.getIdentifier(e.constructor)
        }
        var j = I(U, function(e, t) {
            return ["class", t.classRegistry.getIdentifier(e.constructor)]
        }, function(e, t) {
            var n = t.classRegistry.getAllowedProps(e.constructor);
            if (!n)
                return D({}, e);
            var r = {};
            return n.forEach(function(t) {
                r[t] = e[t]
            }),
            r
        }, function(e, t, n) {
            var r = n.classRegistry.getValue(t[1]);
            if (!r)
                throw Error("Trying to deserialize unknown class - check https://github.com/blitz-js/superjson/issues/116#issuecomment-773996564");
            return Object.assign(Object.create(r.prototype), e)
        })
          , B = I(function(e, t) {
            return !!t.customTransformerRegistry.findApplicable(e)
        }, function(e, t) {
            return ["custom", t.customTransformerRegistry.findApplicable(e).name]
        }, function(e, t) {
            return t.customTransformerRegistry.findApplicable(e).serialize(e)
        }, function(e, t, n) {
            var r = n.customTransformerRegistry.findByName(t[1]);
            if (!r)
                throw Error("Trying to deserialize unknown custom value");
            return r.deserialize(e)
        })
          , Y = [j, P, B, L]
          , M = function(e, t) {
            var n = g(Y, function(n) {
                return n.isApplicable(e, t)
            });
            if (n)
                return {
                    value: n.transform(e, t),
                    type: n.annotation(e, t)
                };
            var r = g($, function(n) {
                return n.isApplicable(e, t)
            });
            if (r)
                return {
                    value: r.transform(e, t),
                    type: r.annotation
                }
        }
          , G = {};
        $.forEach(function(e) {
            G[e.annotation] = e
        });
        var V = function(e, t, n) {
            if (b(t))
                switch (t[0]) {
                case "symbol":
                    return P.untransform(e, t, n);
                case "class":
                    return j.untransform(e, t, n);
                case "custom":
                    return B.untransform(e, t, n);
                case "typed-array":
                    return L.untransform(e, t, n);
                default:
                    throw Error("Unknown transformation: " + t)
                }
            else {
                var r = G[t];
                if (!r)
                    throw Error("Unknown transformation: " + t);
                return r.untransform(e, n)
            }
        }
          , H = function(e, t) {
            for (var n = e.keys(); t > 0; )
                n.next(),
                t--;
            return n.next().value
        };
        function F(e) {
            if (f(e, "__proto__"))
                throw Error("__proto__ is not allowed as a property");
            if (f(e, "prototype"))
                throw Error("prototype is not allowed as a property");
            if (f(e, "constructor"))
                throw Error("constructor is not allowed as a property")
        }
        var z = function(e, t) {
            F(t);
            for (var n = 0; n < t.length; n++) {
                var r = t[n];
                if (E(e))
                    e = H(e, +r);
                else if (S(e)) {
                    var i = +r
                      , o = 0 == +t[++n] ? "key" : "value"
                      , s = H(e, i);
                    switch (o) {
                    case "key":
                        e = s;
                        break;
                    case "value":
                        e = e.get(s)
                    }
                } else
                    e = e[r]
            }
            return e
        }
          , q = function(e, t, n) {
            if (F(t),
            0 === t.length)
                return n(e);
            for (var r = e, i = 0; i < t.length - 1; i++) {
                var o = t[i];
                if (b(r))
                    r = r[+o];
                else if (y(r))
                    r = r[o];
                else if (E(r)) {
                    var s = +o;
                    r = H(r, s)
                } else if (S(r)) {
                    if (i === t.length - 2)
                        break;
                    var s = +o
                      , a = 0 == +t[++i] ? "key" : "value"
                      , l = H(r, s);
                    switch (a) {
                    case "key":
                        r = l;
                        break;
                    case "value":
                        r = r.get(l)
                    }
                }
            }
            var u = t[t.length - 1];
            if (b(r) ? r[+u] = n(r[+u]) : y(r) && (r[u] = n(r[u])),
            E(r)) {
                var c = H(r, +u)
                  , d = n(c);
                c !== d && (r.delete(c),
                r.add(d))
            }
            if (S(r)) {
                var s = +t[t.length - 2]
                  , p = H(r, s)
                  , a = 0 == +u ? "key" : "value";
                switch (a) {
                case "key":
                    var h = n(p);
                    r.set(h, r.get(p)),
                    h !== p && r.delete(p);
                    break;
                case "value":
                    r.set(p, n(r.get(p)))
                }
            }
            return e
        }
          , W = function(e, t) {
            var n = "function" == typeof Symbol && e[Symbol.iterator];
            if (!n)
                return e;
            var r, i, o = n.call(e), s = [];
            try {
                for (; (void 0 === t || t-- > 0) && !(r = o.next()).done; )
                    s.push(r.value)
            } catch (a) {
                i = {
                    error: a
                }
            } finally {
                try {
                    r && !r.done && (n = o.return) && n.call(o)
                } finally {
                    if (i)
                        throw i.error
                }
            }
            return s
        }
          , J = function(e, t) {
            for (var n = 0, r = t.length, i = e.length; n < r; n++,
            i++)
                e[i] = t[n];
            return e
        }
          , K = function(e, t, n, r, i, o, s) {
            void 0 === i && (i = []),
            void 0 === o && (o = []),
            void 0 === s && (s = new Map);
            var a, l, u = "boolean" == typeof (a = e) || null === a || _(a) || "number" == typeof a && !isNaN(a) || "string" == typeof a || w(a);
            if (!u) {
                c = i,
                (d = t.get(e)) ? d.push(c) : t.set(e, [c]);
                var c, d, p = s.get(e);
                if (p)
                    return r ? {
                        transformedValue: null
                    } : p
            }
            if (!(y(e) || b(e) || S(e) || E(e) || U(e, n))) {
                var g = M(e, n)
                  , m = g ? {
                    transformedValue: g.value,
                    annotations: [g.type]
                } : {
                    transformedValue: e
                };
                return u || s.set(e, m),
                m
            }
            if (f(o, e))
                return {
                    transformedValue: null
                };
            var x = M(e, n)
              , k = null !== (l = null == x ? void 0 : x.value) && void 0 !== l ? l : e
              , R = b(k) ? [] : {}
              , D = {};
            h(k, function(a, l) {
                var u = K(a, t, n, r, J(J([], W(i)), [l]), J(J([], W(o)), [e]), s);
                R[l] = u.transformedValue,
                b(u.annotations) ? D[l] = u.annotations : y(u.annotations) && h(u.annotations, function(e, t) {
                    D[T(l) + "." + t] = e
                })
            });
            var O = v(D) ? {
                transformedValue: R,
                annotations: x ? [x.type] : void 0
            } : {
                transformedValue: R,
                annotations: x ? [x.type, D] : D
            };
            return u || s.set(e, O),
            O
        };
        function X(e) {
            return Object.prototype.toString.call(e).slice(8, -1)
        }
        function Z(e) {
            return "Array" === X(e)
        }
        var Q = function() {
            return (Q = Object.assign || function(e) {
                for (var t, n = 1, r = arguments.length; n < r; n++)
                    for (var i in t = arguments[n])
                        Object.prototype.hasOwnProperty.call(t, i) && (e[i] = t[i]);
                return e
            }
            ).apply(this, arguments)
        }
          , ee = function(e, t) {
            var n = "function" == typeof Symbol && e[Symbol.iterator];
            if (!n)
                return e;
            var r, i, o = n.call(e), s = [];
            try {
                for (; (void 0 === t || t-- > 0) && !(r = o.next()).done; )
                    s.push(r.value)
            } catch (a) {
                i = {
                    error: a
                }
            } finally {
                try {
                    r && !r.done && (n = o.return) && n.call(o)
                } finally {
                    if (i)
                        throw i.error
                }
            }
            return s
        }
          , et = function(e, t) {
            for (var n = 0, r = t.length, i = e.length; n < r; n++,
            i++)
                e[i] = t[n];
            return e
        }
          , en = function() {
            function e(e) {
                var t = (void 0 === e ? {} : e).dedupe;
                this.classRegistry = new d,
                this.symbolRegistry = new u(function(e) {
                    var t;
                    return null !== (t = e.description) && void 0 !== t ? t : ""
                }
                ),
                this.customTransformerRegistry = new m,
                this.allowedErrorProps = [],
                this.dedupe = void 0 !== t && t
            }
            return e.prototype.serialize = function(e) {
                var t, n, r = new Map, i = K(e, r, this, this.dedupe), o = {
                    json: i.transformedValue
                };
                i.annotations && (o.meta = Q(Q({}, o.meta), {
                    values: i.annotations
                }));
                var s = (t = {},
                n = void 0,
                (r.forEach(function(e) {
                    if (!(e.length <= 1)) {
                        var r = W(e.map(function(e) {
                            return e.map(String)
                        }).sort(function(e, t) {
                            return e.length - t.length
                        }))
                          , i = r[0]
                          , o = r.slice(1);
                        0 === i.length ? n = o.map(k) : t[k(i)] = o.map(k)
                    }
                }),
                n) ? v(t) ? [n] : [n, t] : v(t) ? void 0 : t);
                return s && (o.meta = Q(Q({}, o.meta), {
                    referentialEqualities: s
                })),
                o
            }
            ,
            e.prototype.deserialize = function(e) {
                var t, n, r, i = e.json, o = e.meta, s = function e(t, n={}) {
                    if (Z(t))
                        return t.map(t=>e(t, n));
                    if (!function(e) {
                        if ("Object" !== X(e))
                            return !1;
                        let t = Object.getPrototypeOf(e);
                        return !!t && t.constructor === Object && t === Object.prototype
                    }(t))
                        return t;
                    let r = Object.getOwnPropertyNames(t)
                      , i = Object.getOwnPropertySymbols(t);
                    return [...r, ...i].reduce((r,i)=>{
                        if (Z(n.props) && !n.props.includes(i))
                            return r;
                        let o = t[i]
                          , s = e(o, n);
                        return function(e, t, n, r, i) {
                            let o = ({}).propertyIsEnumerable.call(r, t) ? "enumerable" : "nonenumerable";
                            "enumerable" === o && (e[t] = n),
                            i && "nonenumerable" === o && Object.defineProperty(e, t, {
                                value: n,
                                enumerable: !1,
                                writable: !0,
                                configurable: !0
                            })
                        }(r, i, s, t, n.nonenumerable),
                        r
                    }
                    , {})
                }(i);
                return (null == o ? void 0 : o.values) && (t = s,
                n = o.values,
                r = this,
                function e(t, n, r) {
                    if (void 0 === r && (r = []),
                    t) {
                        if (!b(t)) {
                            h(t, function(t, i) {
                                return e(t, n, J(J([], W(r)), W(R(i))))
                            });
                            return
                        }
                        var i = W(t, 2)
                          , o = i[0]
                          , s = i[1];
                        s && h(s, function(t, i) {
                            e(t, n, J(J([], W(r)), W(R(i))))
                        }),
                        n(o, r)
                    }
                }(n, function(e, n) {
                    t = q(t, n, function(t) {
                        return V(t, e, r)
                    })
                }),
                s = t),
                (null == o ? void 0 : o.referentialEqualities) && (s = function(e, t) {
                    function n(t, n) {
                        var r = z(e, R(n));
                        t.map(R).forEach(function(t) {
                            e = q(e, t, function() {
                                return r
                            })
                        })
                    }
                    if (b(t)) {
                        var r = W(t, 2)
                          , i = r[0]
                          , o = r[1];
                        i.forEach(function(t) {
                            e = q(e, R(t), function() {
                                return e
                            })
                        }),
                        o && h(o, n)
                    } else
                        h(t, n);
                    return e
                }(s, o.referentialEqualities)),
                s
            }
            ,
            e.prototype.stringify = function(e) {
                return JSON.stringify(this.serialize(e))
            }
            ,
            e.prototype.parse = function(e) {
                return this.deserialize(JSON.parse(e))
            }
            ,
            e.prototype.registerClass = function(e, t) {
                this.classRegistry.register(e, t)
            }
            ,
            e.prototype.registerSymbol = function(e, t) {
                this.symbolRegistry.register(e, t)
            }
            ,
            e.prototype.registerCustom = function(e, t) {
                this.customTransformerRegistry.register(Q({
                    name: t
                }, e))
            }
            ,
            e.prototype.allowErrorProps = function() {
                for (var e, t = [], n = 0; n < arguments.length; n++)
                    t[n] = arguments[n];
                (e = this.allowedErrorProps).push.apply(e, et([], ee(t)))
            }
            ,
            e.defaultInstance = new e,
            e.serialize = e.defaultInstance.serialize.bind(e.defaultInstance),
            e.deserialize = e.defaultInstance.deserialize.bind(e.defaultInstance),
            e.stringify = e.defaultInstance.stringify.bind(e.defaultInstance),
            e.parse = e.defaultInstance.parse.bind(e.defaultInstance),
            e.registerClass = e.defaultInstance.registerClass.bind(e.defaultInstance),
            e.registerSymbol = e.defaultInstance.registerSymbol.bind(e.defaultInstance),
            e.registerCustom = e.defaultInstance.registerCustom.bind(e.defaultInstance),
            e.allowErrorProps = e.defaultInstance.allowErrorProps.bind(e.defaultInstance),
            e
        }();
        en.serialize;
        var er = en.deserialize;
        en.stringify,
        en.parse,
        en.registerClass,
        en.registerCustom,
        en.registerSymbol,
        en.allowErrorProps;
        var ei = n(27484)
          , eo = n.n(ei);
        n(76831),
        n(25054);
        var es = n(29387)
          , ea = n.n(es)
          , el = n(70178)
          , eu = n.n(el)
          , ec = n(64487);
        n(90536);
        let ed = e=>null != e && 0 === Object.keys(e).length;
        var ep = n(11163);
        let eh = function(e) {
            let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : document.title;
            window.gtag("config", "G-K5BMRZW85X", {
                page_path: e,
                page_title: t
            })
        };
        var ef = n(14691)
          , eg = n(19521)
          , em = n(47443)
          , e_ = n(7297)
          , ey = n(76362)
          , ev = function(e, t, n) {
            if (!ey.jU)
                return [t, ey.ZT, ey.ZT];
            if (!e)
                throw Error("useLocalStorage key may not be falsy");
            var r = n ? n.raw ? function(e) {
                return e
            }
            : n.deserializer : JSON.parse
              , i = (0,
            a.useRef)(function(e) {
                try {
                    var i = n ? n.raw ? String : n.serializer : JSON.stringify
                      , o = localStorage.getItem(e);
                    if (null !== o)
                        return r(o);
                    return t && localStorage.setItem(e, i(t)),
                    t
                } catch (s) {
                    return t
                }
            })
              , o = (0,
            a.useState)(function() {
                return i.current(e)
            })
              , s = o[0]
              , l = o[1];
            (0,
            a.useLayoutEffect)(function() {
                return l(i.current(e))
            }, [e]);
            var u = (0,
            a.useCallback)(function(t) {
                try {
                    var i = "function" == typeof t ? t(s) : t;
                    if (void 0 === i)
                        return;
                    var o = void 0;
                    o = n ? n.raw ? "string" == typeof i ? i : JSON.stringify(i) : n.serializer ? n.serializer(i) : JSON.stringify(i) : JSON.stringify(i),
                    localStorage.setItem(e, o),
                    l(r(o))
                } catch (a) {}
            }, [e, l]);
            return [s, u, (0,
            a.useCallback)(function() {
                try {
                    localStorage.removeItem(e),
                    l(void 0)
                } catch (t) {}
            }, [e, l])]
        }
          , eb = n(18127)
          , eS = function(e) {
            (0,
            eb.Z)(function() {
                e()
            })
        }
          , eE = n(75343)
          , ew = n(17527);
        function ex() {
            let e = (0,
            e_.Z)(["\n  to {\n    opacity: 1;\n  }\n"]);
            return ex = function() {
                return e
            }
            ,
            e
        }
        function eT() {
            let e = (0,
            e_.Z)(["\n  z-index: 200;\n  max-width: 480px;\n  position: fixed;\n  display: grid;\n  grid-template-columns: 1fr auto auto;\n  gap: 8px;\n  align-items: center;\n  border-radius: 8px;\n  bottom: env(safe-area-inset-bottom);\n  margin-bottom: calc(8px * 5);\n  right: calc(8px * 5);\n  padding: calc(8px * 3);\n  color: ", ";\n  background-color: ", ";\n  box-shadow: 0px 4px 16px rgba(0, 0, 0, 0.08);\n  ", " {\n    padding: calc(8px * 2);\n    left: calc(8px * 2);\n    right: calc(8px * 2);\n    margin: 0 auto calc(8px * 3 / 2);\n  }\n  opacity: 0;\n  animation: ", " forwards;\n  animation-delay: ", ";\n"]);
            return eT = function() {
                return e
            }
            ,
            e
        }
        function ek() {
            let e = (0,
            e_.Z)(["\n  font-size: ", ";\n  ", " {\n    font-size: ", ";\n    margin-right: 8px;\n  }\n"]);
            return ek = function() {
                return e
            }
            ,
            e
        }
        function eR() {
            let e = (0,
            e_.Z)(["\n  ", "\n"]);
            return eR = function() {
                return e
            }
            ,
            e
        }
        function eD() {
            let e = (0,
            e_.Z)(["\n  ", "\n"]);
            return eD = function() {
                return e
            }
            ,
            e
        }
        function eO() {
            let e = (0,
            e_.Z)(["\n  display: inline-flex;\n  align-items: center;\n  justify-content: space-around;\n  min-width: 40px;\n  min-height: 40px;\n  padding: 0 16px;\n  overflow: hidden;\n  color: ", ";\n  vertical-align: middle;\n  font-family: inherit;\n  font-size: ", ";\n  line-height: ", ";\n  font-weight: bold;\n  text-align: center;\n  background-color: ", ";\n  border: none;\n  border-radius: 20px;\n  outline: none;\n  cursor: pointer;\n  user-select: none;\n\n  svg {\n    font-size: 2em;\n  }\n\n  &:hover {\n    background-color: ", ";\n  }\n\n  &:focus {\n    box-shadow: 0 0 0 4px ", ";\n  }\n\n  &:active {\n    background-color: ", ";\n  }\n\n  ", "\n  ", "\n"]);
            return eO = function() {
                return e
            }
            ,
            e
        }
        function eN() {
            let {t: e} = (0,
            ef.$G)("privacyPolicyUpdate")
              , t = (0,
            ep.useRouter)()
              , [n,r] = (0,
            a.useState)(!1)
              , [i,l] = ev("privacyPolicyAccepted20230613", !1);
            eS(()=>{
                r(!0)
            }
            );
            let u = (0,
            a.useMemo)(()=>"/" == t.pathname ? "3s" : "/studio" === t.pathname ? "4s" : "0", [])
              , c = (0,
            a.useCallback)(()=>l(!0), []);
            return !n || i ? null : (0,
            s.jsxs)(e$, {
                animationDelay: u,
                children: [(0,
                s.jsx)(eI, {
                    children: (0,
                    s.jsxs)(ew.cC, {
                        t: e,
                        i18nKey: "description",
                        children: [(0,
                        s.jsx)("a", {
                            tabIndex: -1,
                            rel: "noreferrer noopener",
                            target: "_blank",
                            href: "https://policies.pixiv.net/#privacy-policy-14"
                        }), (0,
                        s.jsx)("a", {
                            tabIndex: -1,
                            rel: "noreferrer noopener",
                            target: "_blank",
                            href: "https://policies.pixiv.net/#privacy-policy-revision-history"
                        })]
                    })
                }), (0,
                s.jsx)(eL, {
                    kind: o.primary,
                    onClick: c,
                    children: e("agree")
                })]
            })
        }
        let eC = (0,
        eg.F4)(ex())
          , e$ = eg.ZP.div.withConfig({
            displayName: "PrivacyPolicyUpdate__Container",
            componentId: "sc-b6044662-0"
        })(eT(), e=>{
            let {theme: t} = e;
            return t.white
        }
        , e=>{
            let {theme: t} = e;
            return t.gray80
        }
        , eE.BC.smallDown, eC, e=>{
            let {animationDelay: t} = e;
            return t
        }
        )
          , eI = eg.ZP.span.withConfig({
            displayName: "PrivacyPolicyUpdate__PrivacyPolicyUpdateText",
            componentId: "sc-b6044662-1"
        })(ek(), em.D.fontSize.bodyS, eE.BC.smallUp, em.D.fontSize.bodyM);
        (i = o || (o = {}))[i.primary = 0] = "primary",
        i[i.action = 1] = "action";
        let eP = (0,
        eg.iv)(eR(), e=>{
            let {theme: t} = e;
            return "\n    color: ".concat(t.white, ";\n    background-color: ").concat(t.blue50, ";\n\n    &:focus {\n      background-color: ").concat(t.blue50, ";\n    }\n\n    &:hover {\n      background-color: ").concat(t.blue60, ";\n    }\n\n    &:active {\n      background-color: ").concat(t.blue70, ";\n    }\n  ")
        }
        )
          , eA = (0,
        eg.iv)(eD(), e=>{
            let {theme: t} = e;
            return "\n    color: ".concat(t.gray60, ";\n    background-color: ").concat(t.white, ";\n\n    &:focus {\n      background-color: ").concat(t.white, ";\n    }\n\n    &:hover {\n      background-color: ").concat(t.gray20, ";\n    }\n\n    &:active {\n      background-color: ").concat(t.gray30, ";\n    }\n  ")
        }
        )
          , eL = eg.ZP.button.attrs(e=>{
            let {type: t} = e;
            return {
                type: null != t ? t : "button"
            }
        }
        ).withConfig({
            displayName: "PrivacyPolicyUpdate__Button",
            componentId: "sc-b6044662-2"
        })(eO(), e=>{
            let {theme: t} = e;
            return t.blackFade10
        }
        , em.D.fontSize.button, em.D.lineHeight.button, e=>{
            let {theme: t} = e;
            return t.blackFade10
        }
        , e=>{
            let {theme: t} = e;
            return t.blackFade20
        }
        , e=>{
            let {theme: t} = e;
            return "rgba(".concat(t.blue50, ", 0.32)")
        }
        , e=>{
            let {theme: t} = e;
            return t.blackFade30
        }
        , e=>{
            let {kind: t} = e;
            return t === o.primary && eP
        }
        , e=>{
            let {kind: t} = e;
            return t === o.action && eA
        }
        );
        function eU(e) {
            let {Component: t, pageProps: n} = e
              , r = {};
            try {
                let i = n && !ed(n);
                i && (r = er(n))
            } catch (o) {
                setTimeout(()=>{
                    ec.$e(e=>{
                        e.setExtras({
                            pageProps: n
                        }),
                        ec.Tb(o)
                    }
                    )
                }
                )
            }
            let l = (0,
            ep.useRouter)();
            return (0,
            a.useEffect)(()=>{
                let e = e=>{
                    eh(e)
                }
                ;
                return l.events.on("routeChangeComplete", e),
                ()=>l.events.off("routeChangeComplete", e)
            }
            , [l.events]),
            (0,
            s.jsx)(ef.a3, {
                lng: l.locale,
                children: (0,
                s.jsxs)(eg.f6, {
                    theme: em.W,
                    children: [(0,
                    s.jsx)(t, {
                        ...r
                    }), (0,
                    s.jsx)(eN, {})]
                })
            })
        }
        eo().extend(eu()),
        eo().extend(ea()),
        eo().tz.setDefault("Asia/Tokyo"),
        n(66337),
        n(30523).polyfill()
    },
    66979: function(e, t, n) {
        "use strict";
        n.d(t, {
            GS: function() {
                return s
            },
            MQ: function() {
                return a
            },
            Pf: function() {
                return l
            },
            vO: function() {
                return o
            }
        });
        var r = n(67294);
        let i = r.useLayoutEffect
          , o = ()=>{
            let[e,t] = (0,
            r.useState)({
                scrollX: 0,
                scrollY: 0
            });
            return (0,
            r.useEffect)(()=>{
                let e = ()=>t({
                    scrollX: window.scrollX,
                    scrollY: window.scrollY
                });
                return window.addEventListener("scroll", e, {
                    passive: !0
                }),
                ()=>window.removeEventListener("scroll", e)
            }
            , []),
            e
        }
          , s = function() {
            let e = arguments.length > 0 && void 0 !== arguments[0] ? arguments[0] : 800
              , t = "screen and (max-width: ".concat(e, "px)")
              , n = (0,
            r.useRef)(null)
              , [o,s] = (0,
            r.useState)(!1);
            return i(()=>{
                let e = e=>s(e.matches);
                return n.current = matchMedia(t),
                n.current.addListener(e),
                s(n.current.matches),
                ()=>n.current.removeListener(e)
            }
            , []),
            {
                isMobile: o
            }
        }
          , a = e=>{
            let t = (0,
            r.useRef)(null)
              , n = (0,
            r.useRef)(null)
              , i = (0,
            r.useRef)(e)
              , o = (0,
            r.useCallback)(e=>{
                let[t] = e;
                1 === t.intersectionRatio && i.current()
            }
            , []);
            return (0,
            r.useEffect)(()=>(t.current = new IntersectionObserver(o,{
                threshold: 1
            }),
            t.current.observe(n.current),
            ()=>t.current.unobserve(n.current)), []),
            (0,
            r.useEffect)(()=>{
                i.current = e
            }
            , [e]),
            {
                ref: n
            }
        }
          , l = function(e, t) {
            let n = arguments.length > 2 && void 0 !== arguments[2] ? arguments[2] : []
              , i = (0,
            r.useRef)(null);
            (0,
            r.useEffect)(()=>{
                if (null == i.current) {
                    i.current = t;
                    return
                }
                for (let n in t)
                    if (i.current[n] !== t[n])
                        return i.current = t,
                        e()
            }
            , [...t, ...n])
        }
    },
    75343: function(e, t, n) {
        "use strict";
        n.d(t, {
            BC: function() {
                return s
            }
        });
        let r = e=>"@media (max-width: ".concat(e, "px)")
          , i = e=>"@media (min-width: ".concat(e, "px)")
          , o = {
            largeMedium: 1023,
            mediumSmall: 767,
            smallXsmall: 350
        }
          , s = {
            largeUp: i(o.largeMedium + 1),
            mediumUp: i(o.mediumSmall + 1),
            smallUp: i(o.smallXsmall + 1),
            mediumDown: r(o.largeMedium),
            smallDown: r(o.mediumSmall),
            xsmallDown: r(o.smallXsmall)
        };
        var a = n(7297)
          , l = n(19521);
        function u() {
            let e = (0,
            a.Z)(["\n  ", " {\n    display: none;\n  }\n"]);
            return u = function() {
                return e
            }
            ,
            e
        }
        function c() {
            let e = (0,
            a.Z)(["\n  ", " {\n    display: none;\n  }\n"]);
            return c = function() {
                return e
            }
            ,
            e
        }
        l.ZP.br.withConfig({
            displayName: "commonStyled__BrWithMediumUp",
            componentId: "sc-bb0d3f5c-0"
        })(u(), s.smallDown),
        l.ZP.br.withConfig({
            displayName: "commonStyled__BrWithSmallDown",
            componentId: "sc-bb0d3f5c-1"
        })(c(), s.mediumUp)
    },
    47443: function(e, t, n) {
        "use strict";
        n.d(t, {
            D: function() {
                return i
            },
            W: function() {
                return r
            }
        });
        let r = {
            gray10: "#f5f5f5",
            gray20: "#ebebeb",
            gray30: "#d6d6d6",
            gray40: "#adadad",
            gray50: "#858585",
            gray60: "#5c5c5c",
            gray70: "#474747",
            gray80: "#333",
            gray90: "#1f1f1f",
            blackFade10: "rgba(0, 0, 0, .04)",
            blackFade20: "rgba(0, 0, 0, .08)",
            blackFade30: "rgba(0, 0, 0, .16)",
            blackFade40: "rgba(0, 0, 0, .32)",
            blackFade50: "rgba(0, 0, 0, .48)",
            blackFade60: "rgba(0, 0, 0, .64)",
            blackFade90: "rgba(0, 0, 0, .88)",
            blue00: "#e9f5fe",
            blue50: "#0096fa",
            blue60: "#007dd1",
            blue70: "#0066ab",
            black: "#000",
            white: "#fff",
            whiteFade00: "rgba(255, 255, 255, .12)",
            whiteFade50: "rgba(255, 255, 255, .68)",
            red: "#ff2b00",
            r18: "#ff4060",
            adultPale: "#ffecec",
            heart: "#ff4060",
            booth: "#fc4d50"
        }
          , i = {
            size: {
                contentMiddleWidth: "1224px",
                moduleDialog: "440px",
                borderRadius: "4px"
            },
            fontSize: {
                captionS: "12px",
                buttonXs: "12px",
                button: "14px",
                titleXs: "14px",
                titleS: "16px",
                titleM: "20px",
                titleL: "32px",
                bodyM: "16px",
                bodyS: "14px",
                embed: "14px",
                countBadge: "10px",
                artworkCharacter: "10px",
                notificationBadge: "11px",
                iconXs: "14px",
                optimizationStatusCompact: "12px"
            },
            lineHeight: {
                captionS: "16px",
                buttonXs: "16px",
                button: "22px",
                titleXs: "22px",
                titleS: "24px",
                titleM: "28px",
                titleL: "40px",
                bodyM: "24px",
                bodyS: "22px",
                embed: "22px",
                countBadge: "10px",
                artworkCharacter: "14px",
                optimizationStatusCompact: "16px"
            },
            transition: {
                easing: "cubic-bezier(0.215, 0.61, 0.355, 1)",
                duration: "0.24s"
            },
            opacity: {
                disabled: .32
            },
            zIndex: {
                tooltipOnModal: 450,
                modal: 400
            }
        }
    },
    90536: function() {},
    11163: function(e, t, n) {
        e.exports = n(80880)
    },
    34155: function(e) {
        var t, n, r, i = e.exports = {};
        function o() {
            throw Error("setTimeout has not been defined")
        }
        function s() {
            throw Error("clearTimeout has not been defined")
        }
        function a(e) {
            if (t === setTimeout)
                return setTimeout(e, 0);
            if ((t === o || !t) && setTimeout)
                return t = setTimeout,
                setTimeout(e, 0);
            try {
                return t(e, 0)
            } catch (r) {
                try {
                    return t.call(null, e, 0)
                } catch (n) {
                    return t.call(this, e, 0)
                }
            }
        }
        !function() {
            try {
                t = "function" == typeof setTimeout ? setTimeout : o
            } catch (e) {
                t = o
            }
            try {
                n = "function" == typeof clearTimeout ? clearTimeout : s
            } catch (r) {
                n = s
            }
        }();
        var l = []
          , u = !1
          , c = -1;
        function d() {
            u && r && (u = !1,
            r.length ? l = r.concat(l) : c = -1,
            l.length && p())
        }
        function p() {
            if (!u) {
                var e = a(d);
                u = !0;
                for (var t = l.length; t; ) {
                    for (r = l,
                    l = []; ++c < t; )
                        r && r[c].run();
                    c = -1,
                    t = l.length
                }
                r = null,
                u = !1,
                function(e) {
                    if (n === clearTimeout)
                        return clearTimeout(e);
                    if ((n === s || !n) && clearTimeout)
                        return n = clearTimeout,
                        clearTimeout(e);
                    try {
                        n(e)
                    } catch (r) {
                        try {
                            return n.call(null, e)
                        } catch (t) {
                            return n.call(this, e)
                        }
                    }
                }(e)
            }
        }
        function h(e, t) {
            this.fun = e,
            this.array = t
        }
        function f() {}
        i.nextTick = function(e) {
            var t = Array(arguments.length - 1);
            if (arguments.length > 1)
                for (var n = 1; n < arguments.length; n++)
                    t[n - 1] = arguments[n];
            l.push(new h(e,t)),
            1 !== l.length || u || a(p)
        }
        ,
        h.prototype.run = function() {
            this.fun.apply(null, this.array)
        }
        ,
        i.title = "browser",
        i.browser = !0,
        i.env = {},
        i.argv = [],
        i.version = "",
        i.versions = {},
        i.on = f,
        i.addListener = f,
        i.once = f,
        i.off = f,
        i.removeListener = f,
        i.removeAllListeners = f,
        i.emit = f,
        i.prependListener = f,
        i.prependOnceListener = f,
        i.listeners = function(e) {
            return []
        }
        ,
        i.binding = function(e) {
            throw Error("process.binding is not supported")
        }
        ,
        i.cwd = function() {
            return "/"
        }
        ,
        i.chdir = function(e) {
            throw Error("process.chdir is not supported")
        }
        ,
        i.umask = function() {
            return 0
        }
    },
    69921: function(e, t) {
        "use strict";
        /** @license React v16.13.1
 * react-is.production.min.js
 *
 * Copyright (c) Facebook, Inc. and its affiliates.
 *
 * This source code is licensed under the MIT license found in the
 * LICENSE file in the root directory of this source tree.
 */
        var n = "function" == typeof Symbol && Symbol.for
          , r = n ? Symbol.for("react.element") : 60103
          , i = n ? Symbol.for("react.portal") : 60106
          , o = n ? Symbol.for("react.fragment") : 60107
          , s = n ? Symbol.for("react.strict_mode") : 60108
          , a = n ? Symbol.for("react.profiler") : 60114
          , l = n ? Symbol.for("react.provider") : 60109
          , u = n ? Symbol.for("react.context") : 60110
          , c = n ? Symbol.for("react.async_mode") : 60111
          , d = n ? Symbol.for("react.concurrent_mode") : 60111
          , p = n ? Symbol.for("react.forward_ref") : 60112
          , h = n ? Symbol.for("react.suspense") : 60113
          , f = n ? Symbol.for("react.suspense_list") : 60120
          , g = n ? Symbol.for("react.memo") : 60115
          , m = n ? Symbol.for("react.lazy") : 60116
          , _ = n ? Symbol.for("react.block") : 60121
          , y = n ? Symbol.for("react.fundamental") : 60117
          , v = n ? Symbol.for("react.responder") : 60118
          , b = n ? Symbol.for("react.scope") : 60119;
        function S(e) {
            if ("object" == typeof e && null !== e) {
                var t = e.$$typeof;
                switch (t) {
                case r:
                    switch (e = e.type) {
                    case c:
                    case d:
                    case o:
                    case a:
                    case s:
                    case h:
                        return e;
                    default:
                        switch (e = e && e.$$typeof) {
                        case u:
                        case p:
                        case m:
                        case g:
                        case l:
                            return e;
                        default:
                            return t
                        }
                    }
                case i:
                    return t
                }
            }
        }
        function E(e) {
            return S(e) === d
        }
        t.AsyncMode = c,
        t.ConcurrentMode = d,
        t.ContextConsumer = u,
        t.ContextProvider = l,
        t.Element = r,
        t.ForwardRef = p,
        t.Fragment = o,
        t.Lazy = m,
        t.Memo = g,
        t.Portal = i,
        t.Profiler = a,
        t.StrictMode = s,
        t.Suspense = h,
        t.isAsyncMode = function(e) {
            return E(e) || S(e) === c
        }
        ,
        t.isConcurrentMode = E,
        t.isContextConsumer = function(e) {
            return S(e) === u
        }
        ,
        t.isContextProvider = function(e) {
            return S(e) === l
        }
        ,
        t.isElement = function(e) {
            return "object" == typeof e && null !== e && e.$$typeof === r
        }
        ,
        t.isForwardRef = function(e) {
            return S(e) === p
        }
        ,
        t.isFragment = function(e) {
            return S(e) === o
        }
        ,
        t.isLazy = function(e) {
            return S(e) === m
        }
        ,
        t.isMemo = function(e) {
            return S(e) === g
        }
        ,
        t.isPortal = function(e) {
            return S(e) === i
        }
        ,
        t.isProfiler = function(e) {
            return S(e) === a
        }
        ,
        t.isStrictMode = function(e) {
            return S(e) === s
        }
        ,
        t.isSuspense = function(e) {
            return S(e) === h
        }
        ,
        t.isValidElementType = function(e) {
            return "string" == typeof e || "function" == typeof e || e === o || e === d || e === a || e === s || e === h || e === f || "object" == typeof e && null !== e && (e.$$typeof === m || e.$$typeof === g || e.$$typeof === l || e.$$typeof === u || e.$$typeof === p || e.$$typeof === y || e.$$typeof === v || e.$$typeof === b || e.$$typeof === _)
        }
        ,
        t.typeOf = S
    },
    59864: function(e, t, n) {
        "use strict";
        e.exports = n(69921)
    },
    76362: function(e, t, n) {
        "use strict";
        n.d(t, {
            S1: function() {
                return o
            },
            ZT: function() {
                return r
            },
            jU: function() {
                return s
            },
            on: function() {
                return i
            }
        });
        var r = function() {};
        function i(e) {
            for (var t = [], n = 1; n < arguments.length; n++)
                t[n - 1] = arguments[n];
            e && e.addEventListener && e.addEventListener.apply(e, t)
        }
        function o(e) {
            for (var t = [], n = 1; n < arguments.length; n++)
                t[n - 1] = arguments[n];
            e && e.removeEventListener && e.removeEventListener.apply(e, t)
        }
        var s = "undefined" != typeof window
    },
    18127: function(e, t, n) {
        "use strict";
        var r = n(67294);
        t.Z = function(e) {
            (0,
            r.useEffect)(e, [])
        }
    },
    96774: function(e) {
        e.exports = function(e, t, n, r) {
            var i = n ? n.call(r, e, t) : void 0;
            if (void 0 !== i)
                return !!i;
            if (e === t)
                return !0;
            if ("object" != typeof e || !e || "object" != typeof t || !t)
                return !1;
            var o = Object.keys(e)
              , s = Object.keys(t);
            if (o.length !== s.length)
                return !1;
            for (var a = Object.prototype.hasOwnProperty.bind(t), l = 0; l < o.length; l++) {
                var u = o[l];
                if (!a(u))
                    return !1;
                var c = e[u]
                  , d = t[u];
                if (!1 === (i = n ? n.call(r, c, d, u) : void 0) || void 0 === i && c !== d)
                    return !1
            }
            return !0
        }
    },
    30523: function(e) {
        e.exports = {
            polyfill: function() {
                var e, t = window, n = document;
                if (!("scrollBehavior"in n.documentElement.style) || !0 === t.__forceSmoothScrollPolyfill__) {
                    var r = t.HTMLElement || t.Element
                      , i = {
                        scroll: t.scroll || t.scrollTo,
                        scrollBy: t.scrollBy,
                        elementScroll: r.prototype.scroll || a,
                        scrollIntoView: r.prototype.scrollIntoView
                    }
                      , o = t.performance && t.performance.now ? t.performance.now.bind(t.performance) : Date.now
                      , s = (e = t.navigator.userAgent,
                    RegExp("MSIE |Trident/|Edge/").test(e)) ? 1 : 0;
                    t.scroll = t.scrollTo = function() {
                        if (void 0 !== arguments[0]) {
                            if (!0 === l(arguments[0])) {
                                i.scroll.call(t, void 0 !== arguments[0].left ? arguments[0].left : "object" != typeof arguments[0] ? arguments[0] : t.scrollX || t.pageXOffset, void 0 !== arguments[0].top ? arguments[0].top : void 0 !== arguments[1] ? arguments[1] : t.scrollY || t.pageYOffset);
                                return
                            }
                            d.call(t, n.body, void 0 !== arguments[0].left ? ~~arguments[0].left : t.scrollX || t.pageXOffset, void 0 !== arguments[0].top ? ~~arguments[0].top : t.scrollY || t.pageYOffset)
                        }
                    }
                    ,
                    t.scrollBy = function() {
                        if (void 0 !== arguments[0]) {
                            if (l(arguments[0])) {
                                i.scrollBy.call(t, void 0 !== arguments[0].left ? arguments[0].left : "object" != typeof arguments[0] ? arguments[0] : 0, void 0 !== arguments[0].top ? arguments[0].top : void 0 !== arguments[1] ? arguments[1] : 0);
                                return
                            }
                            d.call(t, n.body, ~~arguments[0].left + (t.scrollX || t.pageXOffset), ~~arguments[0].top + (t.scrollY || t.pageYOffset))
                        }
                    }
                    ,
                    r.prototype.scroll = r.prototype.scrollTo = function() {
                        if (void 0 !== arguments[0]) {
                            if (!0 === l(arguments[0])) {
                                if ("number" == typeof arguments[0] && void 0 === arguments[1])
                                    throw SyntaxError("Value could not be converted");
                                i.elementScroll.call(this, void 0 !== arguments[0].left ? ~~arguments[0].left : "object" != typeof arguments[0] ? ~~arguments[0] : this.scrollLeft, void 0 !== arguments[0].top ? ~~arguments[0].top : void 0 !== arguments[1] ? ~~arguments[1] : this.scrollTop);
                                return
                            }
                            var e = arguments[0].left
                              , t = arguments[0].top;
                            d.call(this, this, void 0 === e ? this.scrollLeft : ~~e, void 0 === t ? this.scrollTop : ~~t)
                        }
                    }
                    ,
                    r.prototype.scrollBy = function() {
                        if (void 0 !== arguments[0]) {
                            if (!0 === l(arguments[0])) {
                                i.elementScroll.call(this, void 0 !== arguments[0].left ? ~~arguments[0].left + this.scrollLeft : ~~arguments[0] + this.scrollLeft, void 0 !== arguments[0].top ? ~~arguments[0].top + this.scrollTop : ~~arguments[1] + this.scrollTop);
                                return
                            }
                            this.scroll({
                                left: ~~arguments[0].left + this.scrollLeft,
                                top: ~~arguments[0].top + this.scrollTop,
                                behavior: arguments[0].behavior
                            })
                        }
                    }
                    ,
                    r.prototype.scrollIntoView = function() {
                        if (!0 === l(arguments[0])) {
                            i.scrollIntoView.call(this, void 0 === arguments[0] || arguments[0]);
                            return
                        }
                        var e = function(e) {
                            for (var t, r, i; e !== n.body && !1 === (r = u(t = e, "Y") && c(t, "Y"),
                            i = u(t, "X") && c(t, "X"),
                            r || i); )
                                e = e.parentNode || e.host;
                            return e
                        }(this)
                          , r = e.getBoundingClientRect()
                          , o = this.getBoundingClientRect();
                        e !== n.body ? (d.call(this, e, e.scrollLeft + o.left - r.left, e.scrollTop + o.top - r.top),
                        "fixed" !== t.getComputedStyle(e).position && t.scrollBy({
                            left: r.left,
                            top: r.top,
                            behavior: "smooth"
                        })) : t.scrollBy({
                            left: o.left,
                            top: o.top,
                            behavior: "smooth"
                        })
                    }
                }
                function a(e, t) {
                    this.scrollLeft = e,
                    this.scrollTop = t
                }
                function l(e) {
                    if (null === e || "object" != typeof e || void 0 === e.behavior || "auto" === e.behavior || "instant" === e.behavior)
                        return !0;
                    if ("object" == typeof e && "smooth" === e.behavior)
                        return !1;
                    throw TypeError("behavior member of ScrollOptions " + e.behavior + " is not a valid value for enumeration ScrollBehavior.")
                }
                function u(e, t) {
                    return "Y" === t ? e.clientHeight + s < e.scrollHeight : "X" === t ? e.clientWidth + s < e.scrollWidth : void 0
                }
                function c(e, n) {
                    var r = t.getComputedStyle(e, null)["overflow" + n];
                    return "auto" === r || "scroll" === r
                }
                function d(e, r, s) {
                    var l, u, c, d, p = o();
                    e === n.body ? (l = t,
                    u = t.scrollX || t.pageXOffset,
                    c = t.scrollY || t.pageYOffset,
                    d = i.scroll) : (l = e,
                    u = e.scrollLeft,
                    c = e.scrollTop,
                    d = a),
                    function e(n) {
                        var r, i, s, a = (o() - n.startTime) / 468;
                        r = .5 * (1 - Math.cos(Math.PI * (a = a > 1 ? 1 : a))),
                        i = n.startX + (n.x - n.startX) * r,
                        s = n.startY + (n.y - n.startY) * r,
                        n.method.call(n.scrollable, i, s),
                        (i !== n.x || s !== n.y) && t.requestAnimationFrame(e.bind(t, n))
                    }({
                        scrollable: l,
                        method: d,
                        startTime: p,
                        startX: u,
                        startY: c,
                        x: r,
                        y: s
                    })
                }
            }
        }
    },
    19521: function(e, t, n) {
        "use strict";
        n.d(t, {
            f6: function() {
                return eR
            },
            iv: function() {
                return ev
            },
            ZP: function() {
                return eC
            },
            F4: function() {
                return eN
            }
        });
        var r, i, o, s = n(59864), a = n(67294), l = n(96774), u = n.n(l), c = function(e) {
            function t(e, t, r) {
                var i = t.trim().split(f);
                t = i;
                var o = i.length
                  , s = e.length;
                switch (s) {
                case 0:
                case 1:
                    var a = 0;
                    for (e = 0 === s ? "" : e[0] + " "; a < o; ++a)
                        t[a] = n(e, t[a], r).trim();
                    break;
                default:
                    var l = a = 0;
                    for (t = []; a < o; ++a)
                        for (var u = 0; u < s; ++u)
                            t[l++] = n(e[u] + " ", i[a], r).trim()
                }
                return t
            }
            function n(e, t, n) {
                var r = t.charCodeAt(0);
                switch (33 > r && (r = (t = t.trim()).charCodeAt(0)),
                r) {
                case 38:
                    return t.replace(g, "$1" + e.trim());
                case 58:
                    return e.trim() + t.replace(g, "$1" + e.trim());
                default:
                    if (0 < 1 * n && 0 < t.indexOf("\f"))
                        return t.replace(g, (58 === e.charCodeAt(0) ? "" : "$1") + e.trim())
                }
                return e + t
            }
            function r(e, t, n, o) {
                var s = e + ";"
                  , a = 2 * t + 3 * n + 4 * o;
                if (944 === a) {
                    e = s.indexOf(":", 9) + 1;
                    var l = s.substring(e, s.length - 1).trim();
                    return l = s.substring(0, e).trim() + l + ";",
                    1 === O || 2 === O && i(l, 1) ? "-webkit-" + l + l : l
                }
                if (0 === O || 2 === O && !i(s, 1))
                    return s;
                switch (a) {
                case 1015:
                    return 97 === s.charCodeAt(10) ? "-webkit-" + s + s : s;
                case 951:
                    return 116 === s.charCodeAt(3) ? "-webkit-" + s + s : s;
                case 963:
                    return 110 === s.charCodeAt(5) ? "-webkit-" + s + s : s;
                case 1009:
                    if (100 !== s.charCodeAt(4))
                        break;
                case 969:
                case 942:
                    return "-webkit-" + s + s;
                case 978:
                    return "-webkit-" + s + "-moz-" + s + s;
                case 1019:
                case 983:
                    return "-webkit-" + s + "-moz-" + s + "-ms-" + s + s;
                case 883:
                    if (45 === s.charCodeAt(8))
                        return "-webkit-" + s + s;
                    if (0 < s.indexOf("image-set(", 11))
                        return s.replace(T, "$1-webkit-$2") + s;
                    break;
                case 932:
                    if (45 === s.charCodeAt(4))
                        switch (s.charCodeAt(5)) {
                        case 103:
                            return "-webkit-box-" + s.replace("-grow", "") + "-webkit-" + s + "-ms-" + s.replace("grow", "positive") + s;
                        case 115:
                            return "-webkit-" + s + "-ms-" + s.replace("shrink", "negative") + s;
                        case 98:
                            return "-webkit-" + s + "-ms-" + s.replace("basis", "preferred-size") + s
                        }
                    return "-webkit-" + s + "-ms-" + s + s;
                case 964:
                    return "-webkit-" + s + "-ms-flex-" + s + s;
                case 1023:
                    if (99 !== s.charCodeAt(8))
                        break;
                    return "-webkit-box-pack" + (l = s.substring(s.indexOf(":", 15)).replace("flex-", "").replace("space-between", "justify")) + "-webkit-" + s + "-ms-flex-pack" + l + s;
                case 1005:
                    return p.test(s) ? s.replace(d, ":-webkit-") + s.replace(d, ":-moz-") + s : s;
                case 1e3:
                    switch (t = (l = s.substring(13).trim()).indexOf("-") + 1,
                    l.charCodeAt(0) + l.charCodeAt(t)) {
                    case 226:
                        l = s.replace(v, "tb");
                        break;
                    case 232:
                        l = s.replace(v, "tb-rl");
                        break;
                    case 220:
                        l = s.replace(v, "lr");
                        break;
                    default:
                        return s
                    }
                    return "-webkit-" + s + "-ms-" + l + s;
                case 1017:
                    if (-1 === s.indexOf("sticky", 9))
                        break;
                case 975:
                    switch (t = (s = e).length - 10,
                    a = (l = (33 === s.charCodeAt(t) ? s.substring(0, t) : s).substring(e.indexOf(":", 7) + 1).trim()).charCodeAt(0) + (0 | l.charCodeAt(7))) {
                    case 203:
                        if (111 > l.charCodeAt(8))
                            break;
                    case 115:
                        s = s.replace(l, "-webkit-" + l) + ";" + s;
                        break;
                    case 207:
                    case 102:
                        s = s.replace(l, "-webkit-" + (102 < a ? "inline-" : "") + "box") + ";" + s.replace(l, "-webkit-" + l) + ";" + s.replace(l, "-ms-" + l + "box") + ";" + s
                    }
                    return s + ";";
                case 938:
                    if (45 === s.charCodeAt(5))
                        switch (s.charCodeAt(6)) {
                        case 105:
                            return l = s.replace("-items", ""),
                            "-webkit-" + s + "-webkit-box-" + l + "-ms-flex-" + l + s;
                        case 115:
                            return "-webkit-" + s + "-ms-flex-item-" + s.replace(E, "") + s;
                        default:
                            return "-webkit-" + s + "-ms-flex-line-pack" + s.replace("align-content", "").replace(E, "") + s
                        }
                    break;
                case 973:
                case 989:
                    if (45 !== s.charCodeAt(3) || 122 === s.charCodeAt(4))
                        break;
                case 931:
                case 953:
                    if (!0 === x.test(e))
                        return 115 === (l = e.substring(e.indexOf(":") + 1)).charCodeAt(0) ? r(e.replace("stretch", "fill-available"), t, n, o).replace(":fill-available", ":stretch") : s.replace(l, "-webkit-" + l) + s.replace(l, "-moz-" + l.replace("fill-", "")) + s;
                    break;
                case 962:
                    if (s = "-webkit-" + s + (102 === s.charCodeAt(5) ? "-ms-" + s : "") + s,
                    211 === n + o && 105 === s.charCodeAt(13) && 0 < s.indexOf("transform", 10))
                        return s.substring(0, s.indexOf(";", 27) + 1).replace(h, "$1-webkit-$2") + s
                }
                return s
            }
            function i(e, t) {
                var n = e.indexOf(1 === t ? ":" : "{")
                  , r = e.substring(0, 3 !== t ? n : 10);
                return n = e.substring(n + 1, e.length - 1),
                I(2 !== t ? r : r.replace(w, "$1"), n, t)
            }
            function o(e, t) {
                var n = r(t, t.charCodeAt(0), t.charCodeAt(1), t.charCodeAt(2));
                return n !== t + ";" ? n.replace(S, " or ($1)").substring(4) : "(" + t + ")"
            }
            function s(e, t, n, r, i, o, s, a, u, c) {
                for (var d, p = 0, h = t; p < $; ++p)
                    switch (d = C[p].call(l, e, h, n, r, i, o, s, a, u, c)) {
                    case void 0:
                    case !1:
                    case !0:
                    case null:
                        break;
                    default:
                        h = d
                    }
                if (h !== t)
                    return h
            }
            function a(e) {
                return void 0 !== (e = e.prefix) && (I = null,
                e ? "function" != typeof e ? O = 1 : (O = 2,
                I = e) : O = 0),
                a
            }
            function l(e, n) {
                var a = e;
                if (33 > a.charCodeAt(0) && (a = a.trim()),
                a = [a],
                0 < $) {
                    var l = s(-1, n, a, a, R, k, 0, 0, 0, 0);
                    void 0 !== l && "string" == typeof l && (n = l)
                }
                var d = function e(n, a, l, d, p) {
                    for (var h, f, g, v, S, E = 0, w = 0, x = 0, T = 0, C = 0, I = 0, A = g = h = 0, L = 0, U = 0, j = 0, B = 0, Y = l.length, M = Y - 1, G = "", V = "", H = "", F = ""; L < Y; ) {
                        if (f = l.charCodeAt(L),
                        L === M && 0 !== w + T + x + E && (0 !== w && (f = 47 === w ? 10 : 47),
                        T = x = E = 0,
                        Y++,
                        M++),
                        0 === w + T + x + E) {
                            if (L === M && (0 < U && (G = G.replace(c, "")),
                            0 < G.trim().length)) {
                                switch (f) {
                                case 32:
                                case 9:
                                case 59:
                                case 13:
                                case 10:
                                    break;
                                default:
                                    G += l.charAt(L)
                                }
                                f = 59
                            }
                            switch (f) {
                            case 123:
                                for (h = (G = G.trim()).charCodeAt(0),
                                g = 1,
                                B = ++L; L < Y; ) {
                                    switch (f = l.charCodeAt(L)) {
                                    case 123:
                                        g++;
                                        break;
                                    case 125:
                                        g--;
                                        break;
                                    case 47:
                                        switch (f = l.charCodeAt(L + 1)) {
                                        case 42:
                                        case 47:
                                            e: {
                                                for (A = L + 1; A < M; ++A)
                                                    switch (l.charCodeAt(A)) {
                                                    case 47:
                                                        if (42 === f && 42 === l.charCodeAt(A - 1) && L + 2 !== A) {
                                                            L = A + 1;
                                                            break e
                                                        }
                                                        break;
                                                    case 10:
                                                        if (47 === f) {
                                                            L = A + 1;
                                                            break e
                                                        }
                                                    }
                                                L = A
                                            }
                                        }
                                        break;
                                    case 91:
                                        f++;
                                    case 40:
                                        f++;
                                    case 34:
                                    case 39:
                                        for (; L++ < M && l.charCodeAt(L) !== f; )
                                            ;
                                    }
                                    if (0 === g)
                                        break;
                                    L++
                                }
                                if (g = l.substring(B, L),
                                0 === h && (h = (G = G.replace(u, "").trim()).charCodeAt(0)),
                                64 === h) {
                                    switch (0 < U && (G = G.replace(c, "")),
                                    f = G.charCodeAt(1)) {
                                    case 100:
                                    case 109:
                                    case 115:
                                    case 45:
                                        U = a;
                                        break;
                                    default:
                                        U = N
                                    }
                                    if (B = (g = e(a, U, g, f, p + 1)).length,
                                    0 < $ && (U = t(N, G, j),
                                    S = s(3, g, U, a, R, k, B, f, p, d),
                                    G = U.join(""),
                                    void 0 !== S && 0 === (B = (g = S.trim()).length) && (f = 0,
                                    g = "")),
                                    0 < B)
                                        switch (f) {
                                        case 115:
                                            G = G.replace(b, o);
                                        case 100:
                                        case 109:
                                        case 45:
                                            g = G + "{" + g + "}";
                                            break;
                                        case 107:
                                            g = (G = G.replace(m, "$1 $2")) + "{" + g + "}",
                                            g = 1 === O || 2 === O && i("@" + g, 3) ? "@-webkit-" + g + "@" + g : "@" + g;
                                            break;
                                        default:
                                            g = G + g,
                                            112 === d && (V += g,
                                            g = "")
                                        }
                                    else
                                        g = ""
                                } else
                                    g = e(a, t(a, G, j), g, d, p + 1);
                                H += g,
                                g = j = U = A = h = 0,
                                G = "",
                                f = l.charCodeAt(++L);
                                break;
                            case 125:
                            case 59:
                                if (1 < (B = (G = (0 < U ? G.replace(c, "") : G).trim()).length))
                                    switch (0 === A && (45 === (h = G.charCodeAt(0)) || 96 < h && 123 > h) && (B = (G = G.replace(" ", ":")).length),
                                    0 < $ && void 0 !== (S = s(1, G, a, n, R, k, V.length, d, p, d)) && 0 === (B = (G = S.trim()).length) && (G = "\0\0"),
                                    h = G.charCodeAt(0),
                                    f = G.charCodeAt(1),
                                    h) {
                                    case 0:
                                        break;
                                    case 64:
                                        if (105 === f || 99 === f) {
                                            F += G + l.charAt(L);
                                            break
                                        }
                                    default:
                                        58 !== G.charCodeAt(B - 1) && (V += r(G, h, f, G.charCodeAt(2)))
                                    }
                                j = U = A = h = 0,
                                G = "",
                                f = l.charCodeAt(++L)
                            }
                        }
                        switch (f) {
                        case 13:
                        case 10:
                            47 === w ? w = 0 : 0 === 1 + h && 107 !== d && 0 < G.length && (U = 1,
                            G += "\0"),
                            0 < $ * P && s(0, G, a, n, R, k, V.length, d, p, d),
                            k = 1,
                            R++;
                            break;
                        case 59:
                        case 125:
                            if (0 === w + T + x + E) {
                                k++;
                                break
                            }
                        default:
                            switch (k++,
                            v = l.charAt(L),
                            f) {
                            case 9:
                            case 32:
                                if (0 === T + E + w)
                                    switch (C) {
                                    case 44:
                                    case 58:
                                    case 9:
                                    case 32:
                                        v = "";
                                        break;
                                    default:
                                        32 !== f && (v = " ")
                                    }
                                break;
                            case 0:
                                v = "\\0";
                                break;
                            case 12:
                                v = "\\f";
                                break;
                            case 11:
                                v = "\\v";
                                break;
                            case 38:
                                0 === T + w + E && (U = j = 1,
                                v = "\f" + v);
                                break;
                            case 108:
                                if (0 === T + w + E + D && 0 < A)
                                    switch (L - A) {
                                    case 2:
                                        112 === C && 58 === l.charCodeAt(L - 3) && (D = C);
                                    case 8:
                                        111 === I && (D = I)
                                    }
                                break;
                            case 58:
                                0 === T + w + E && (A = L);
                                break;
                            case 44:
                                0 === w + x + T + E && (U = 1,
                                v += "\r");
                                break;
                            case 34:
                            case 39:
                                0 === w && (T = T === f ? 0 : 0 === T ? f : T);
                                break;
                            case 91:
                                0 === T + w + x && E++;
                                break;
                            case 93:
                                0 === T + w + x && E--;
                                break;
                            case 41:
                                0 === T + w + E && x--;
                                break;
                            case 40:
                                0 === T + w + E && (0 === h && (2 * C + 3 * I == 533 || (h = 1)),
                                x++);
                                break;
                            case 64:
                                0 === w + x + T + E + A + g && (g = 1);
                                break;
                            case 42:
                            case 47:
                                if (!(0 < T + E + x))
                                    switch (w) {
                                    case 0:
                                        switch (2 * f + 3 * l.charCodeAt(L + 1)) {
                                        case 235:
                                            w = 47;
                                            break;
                                        case 220:
                                            B = L,
                                            w = 42
                                        }
                                        break;
                                    case 42:
                                        47 === f && 42 === C && B + 2 !== L && (33 === l.charCodeAt(B + 2) && (V += l.substring(B, L + 1)),
                                        v = "",
                                        w = 0)
                                    }
                            }
                            0 === w && (G += v)
                        }
                        I = C,
                        C = f,
                        L++
                    }
                    if (0 < (B = V.length)) {
                        if (U = a,
                        0 < $ && void 0 !== (S = s(2, V, U, n, R, k, B, d, p, d)) && 0 === (V = S).length)
                            return F + V + H;
                        if (V = U.join(",") + "{" + V + "}",
                        0 != O * D) {
                            switch (2 !== O || i(V, 2) || (D = 0),
                            D) {
                            case 111:
                                V = V.replace(y, ":-moz-$1") + V;
                                break;
                            case 112:
                                V = V.replace(_, "::-webkit-input-$1") + V.replace(_, "::-moz-$1") + V.replace(_, ":-ms-input-$1") + V
                            }
                            D = 0
                        }
                    }
                    return F + V + H
                }(N, a, n, 0, 0);
                return 0 < $ && void 0 !== (l = s(-2, d, a, a, R, k, d.length, 0, 0, 0)) && (d = l),
                D = 0,
                k = R = 1,
                d
            }
            var u = /^\0+/g
              , c = /[\0\r\f]/g
              , d = /: */g
              , p = /zoo|gra/
              , h = /([,: ])(transform)/g
              , f = /,\r+?/g
              , g = /([\t\r\n ])*\f?&/g
              , m = /@(k\w+)\s*(\S*)\s*/
              , _ = /::(place)/g
              , y = /:(read-only)/g
              , v = /[svh]\w+-[tblr]{2}/
              , b = /\(\s*(.*)\s*\)/g
              , S = /([\s\S]*?);/g
              , E = /-self|flex-/g
              , w = /[^]*?(:[rp][el]a[\w-]+)[^]*/
              , x = /stretch|:\s*\w+\-(?:conte|avail)/
              , T = /([^-])(image-set\()/
              , k = 1
              , R = 1
              , D = 0
              , O = 1
              , N = []
              , C = []
              , $ = 0
              , I = null
              , P = 0;
            return l.use = function e(t) {
                switch (t) {
                case void 0:
                case null:
                    $ = C.length = 0;
                    break;
                default:
                    if ("function" == typeof t)
                        C[$++] = t;
                    else if ("object" == typeof t)
                        for (var n = 0, r = t.length; n < r; ++n)
                            e(t[n]);
                    else
                        P = 0 | !!t
                }
                return e
            }
            ,
            l.set = a,
            void 0 !== e && a(e),
            l
        }, d = {
            animationIterationCount: 1,
            borderImageOutset: 1,
            borderImageSlice: 1,
            borderImageWidth: 1,
            boxFlex: 1,
            boxFlexGroup: 1,
            boxOrdinalGroup: 1,
            columnCount: 1,
            columns: 1,
            flex: 1,
            flexGrow: 1,
            flexPositive: 1,
            flexShrink: 1,
            flexNegative: 1,
            flexOrder: 1,
            gridRow: 1,
            gridRowEnd: 1,
            gridRowSpan: 1,
            gridRowStart: 1,
            gridColumn: 1,
            gridColumnEnd: 1,
            gridColumnSpan: 1,
            gridColumnStart: 1,
            msGridRow: 1,
            msGridRowSpan: 1,
            msGridColumn: 1,
            msGridColumnSpan: 1,
            fontWeight: 1,
            lineHeight: 1,
            opacity: 1,
            order: 1,
            orphans: 1,
            tabSize: 1,
            widows: 1,
            zIndex: 1,
            zoom: 1,
            WebkitLineClamp: 1,
            fillOpacity: 1,
            floodOpacity: 1,
            stopOpacity: 1,
            strokeDasharray: 1,
            strokeDashoffset: 1,
            strokeMiterlimit: 1,
            strokeOpacity: 1,
            strokeWidth: 1
        }, p = /^((children|dangerouslySetInnerHTML|key|ref|autoFocus|defaultValue|defaultChecked|innerHTML|suppressContentEditableWarning|suppressHydrationWarning|valueLink|abbr|accept|acceptCharset|accessKey|action|allow|allowUserMedia|allowPaymentRequest|allowFullScreen|allowTransparency|alt|async|autoComplete|autoPlay|capture|cellPadding|cellSpacing|challenge|charSet|checked|cite|classID|className|cols|colSpan|content|contentEditable|contextMenu|controls|controlsList|coords|crossOrigin|data|dateTime|decoding|default|defer|dir|disabled|disablePictureInPicture|download|draggable|encType|enterKeyHint|form|formAction|formEncType|formMethod|formNoValidate|formTarget|frameBorder|headers|height|hidden|high|href|hrefLang|htmlFor|httpEquiv|id|inputMode|integrity|is|keyParams|keyType|kind|label|lang|list|loading|loop|low|marginHeight|marginWidth|max|maxLength|media|mediaGroup|method|min|minLength|multiple|muted|name|nonce|noValidate|open|optimum|pattern|placeholder|playsInline|poster|preload|profile|radioGroup|readOnly|referrerPolicy|rel|required|reversed|role|rows|rowSpan|sandbox|scope|scoped|scrolling|seamless|selected|shape|size|sizes|slot|span|spellCheck|src|srcDoc|srcLang|srcSet|start|step|style|summary|tabIndex|target|title|translate|type|useMap|value|width|wmode|wrap|about|datatype|inlist|prefix|property|resource|typeof|vocab|autoCapitalize|autoCorrect|autoSave|color|incremental|fallback|inert|itemProp|itemScope|itemType|itemID|itemRef|on|option|results|security|unselectable|accentHeight|accumulate|additive|alignmentBaseline|allowReorder|alphabetic|amplitude|arabicForm|ascent|attributeName|attributeType|autoReverse|azimuth|baseFrequency|baselineShift|baseProfile|bbox|begin|bias|by|calcMode|capHeight|clip|clipPathUnits|clipPath|clipRule|colorInterpolation|colorInterpolationFilters|colorProfile|colorRendering|contentScriptType|contentStyleType|cursor|cx|cy|d|decelerate|descent|diffuseConstant|direction|display|divisor|dominantBaseline|dur|dx|dy|edgeMode|elevation|enableBackground|end|exponent|externalResourcesRequired|fill|fillOpacity|fillRule|filter|filterRes|filterUnits|floodColor|floodOpacity|focusable|fontFamily|fontSize|fontSizeAdjust|fontStretch|fontStyle|fontVariant|fontWeight|format|from|fr|fx|fy|g1|g2|glyphName|glyphOrientationHorizontal|glyphOrientationVertical|glyphRef|gradientTransform|gradientUnits|hanging|horizAdvX|horizOriginX|ideographic|imageRendering|in|in2|intercept|k|k1|k2|k3|k4|kernelMatrix|kernelUnitLength|kerning|keyPoints|keySplines|keyTimes|lengthAdjust|letterSpacing|lightingColor|limitingConeAngle|local|markerEnd|markerMid|markerStart|markerHeight|markerUnits|markerWidth|mask|maskContentUnits|maskUnits|mathematical|mode|numOctaves|offset|opacity|operator|order|orient|orientation|origin|overflow|overlinePosition|overlineThickness|panose1|paintOrder|pathLength|patternContentUnits|patternTransform|patternUnits|pointerEvents|points|pointsAtX|pointsAtY|pointsAtZ|preserveAlpha|preserveAspectRatio|primitiveUnits|r|radius|refX|refY|renderingIntent|repeatCount|repeatDur|requiredExtensions|requiredFeatures|restart|result|rotate|rx|ry|scale|seed|shapeRendering|slope|spacing|specularConstant|specularExponent|speed|spreadMethod|startOffset|stdDeviation|stemh|stemv|stitchTiles|stopColor|stopOpacity|strikethroughPosition|strikethroughThickness|string|stroke|strokeDasharray|strokeDashoffset|strokeLinecap|strokeLinejoin|strokeMiterlimit|strokeOpacity|strokeWidth|surfaceScale|systemLanguage|tableValues|targetX|targetY|textAnchor|textDecoration|textRendering|textLength|to|transform|u1|u2|underlinePosition|underlineThickness|unicode|unicodeBidi|unicodeRange|unitsPerEm|vAlphabetic|vHanging|vIdeographic|vMathematical|values|vectorEffect|version|vertAdvY|vertOriginX|vertOriginY|viewBox|viewTarget|visibility|widths|wordSpacing|writingMode|x|xHeight|x1|x2|xChannelSelector|xlinkActuate|xlinkArcrole|xlinkHref|xlinkRole|xlinkShow|xlinkTitle|xlinkType|xmlBase|xmlns|xmlnsXlink|xmlLang|xmlSpace|y|y1|y2|yChannelSelector|z|zoomAndPan|for|class|autofocus)|(([Dd][Aa][Tt][Aa]|[Aa][Rr][Ii][Aa]|x)-.*))$/, h = (r = Object.create(null),
        function(e) {
            return void 0 === r[e] && (r[e] = p.test(e) || 111 === e.charCodeAt(0) && 110 === e.charCodeAt(1) && 91 > e.charCodeAt(2)),
            r[e]
        }
        ), f = n(8679), g = n.n(f), m = n(34155);
        function _() {
            return (_ = Object.assign || function(e) {
                for (var t = 1; t < arguments.length; t++) {
                    var n = arguments[t];
                    for (var r in n)
                        Object.prototype.hasOwnProperty.call(n, r) && (e[r] = n[r])
                }
                return e
            }
            ).apply(this, arguments)
        }
        var y = function(e, t) {
            for (var n = [e[0]], r = 0, i = t.length; r < i; r += 1)
                n.push(t[r], e[r + 1]);
            return n
        }
          , v = function(e) {
            return null !== e && "object" == typeof e && "[object Object]" === (e.toString ? e.toString() : Object.prototype.toString.call(e)) && !(0,
            s.typeOf)(e)
        }
          , b = Object.freeze([])
          , S = Object.freeze({});
        function E(e) {
            return "function" == typeof e
        }
        function w(e) {
            return e.displayName || e.name || "Component"
        }
        function x(e) {
            return e && "string" == typeof e.styledComponentId
        }
        var T = void 0 !== m && (m.env.REACT_APP_SC_ATTR || m.env.SC_ATTR) || "data-styled"
          , k = "undefined" != typeof window && "HTMLElement"in window
          , R = Boolean("boolean" == typeof SC_DISABLE_SPEEDY ? SC_DISABLE_SPEEDY : void 0 !== m && void 0 !== m.env.REACT_APP_SC_DISABLE_SPEEDY && "" !== m.env.REACT_APP_SC_DISABLE_SPEEDY ? "false" !== m.env.REACT_APP_SC_DISABLE_SPEEDY && m.env.REACT_APP_SC_DISABLE_SPEEDY : void 0 !== m && void 0 !== m.env.SC_DISABLE_SPEEDY && "" !== m.env.SC_DISABLE_SPEEDY && "false" !== m.env.SC_DISABLE_SPEEDY && m.env.SC_DISABLE_SPEEDY);
        function D(e) {
            for (var t = arguments.length, n = Array(t > 1 ? t - 1 : 0), r = 1; r < t; r++)
                n[r - 1] = arguments[r];
            throw Error("An error occurred. See https://git.io/JUIaE#" + e + " for more information." + (n.length > 0 ? " Args: " + n.join(", ") : ""))
        }
        var O = function() {
            function e(e) {
                this.groupSizes = new Uint32Array(512),
                this.length = 512,
                this.tag = e
            }
            var t = e.prototype;
            return t.indexOfGroup = function(e) {
                for (var t = 0, n = 0; n < e; n++)
                    t += this.groupSizes[n];
                return t
            }
            ,
            t.insertRules = function(e, t) {
                if (e >= this.groupSizes.length) {
                    for (var n = this.groupSizes, r = n.length, i = r; e >= i; )
                        (i <<= 1) < 0 && D(16, "" + e);
                    this.groupSizes = new Uint32Array(i),
                    this.groupSizes.set(n),
                    this.length = i;
                    for (var o = r; o < i; o++)
                        this.groupSizes[o] = 0
                }
                for (var s = this.indexOfGroup(e + 1), a = 0, l = t.length; a < l; a++)
                    this.tag.insertRule(s, t[a]) && (this.groupSizes[e]++,
                    s++)
            }
            ,
            t.clearGroup = function(e) {
                if (e < this.length) {
                    var t = this.groupSizes[e]
                      , n = this.indexOfGroup(e)
                      , r = n + t;
                    this.groupSizes[e] = 0;
                    for (var i = n; i < r; i++)
                        this.tag.deleteRule(n)
                }
            }
            ,
            t.getGroup = function(e) {
                var t = "";
                if (e >= this.length || 0 === this.groupSizes[e])
                    return t;
                for (var n = this.groupSizes[e], r = this.indexOfGroup(e), i = r + n, o = r; o < i; o++)
                    t += this.tag.getRule(o) + "/*!sc*/\n";
                return t
            }
            ,
            e
        }()
          , N = new Map
          , C = new Map
          , $ = 1
          , I = function(e) {
            if (N.has(e))
                return N.get(e);
            for (; C.has($); )
                $++;
            var t = $++;
            return N.set(e, t),
            C.set(t, e),
            t
        }
          , P = function(e, t) {
            t >= $ && ($ = t + 1),
            N.set(e, t),
            C.set(t, e)
        }
          , A = "style[" + T + '][data-styled-version="5.3.6"]'
          , L = RegExp("^" + T + '\\.g(\\d+)\\[id="([\\w\\d-]+)"\\].*?"([^"]*)')
          , U = function(e, t, n) {
            for (var r, i = n.split(","), o = 0, s = i.length; o < s; o++)
                (r = i[o]) && e.registerName(t, r)
        }
          , j = function(e, t) {
            for (var n = (t.textContent || "").split("/*!sc*/\n"), r = [], i = 0, o = n.length; i < o; i++) {
                var s = n[i].trim();
                if (s) {
                    var a = s.match(L);
                    if (a) {
                        var l = 0 | parseInt(a[1], 10)
                          , u = a[2];
                        0 !== l && (P(u, l),
                        U(e, u, a[3]),
                        e.getTag().insertRules(l, r)),
                        r.length = 0
                    } else
                        r.push(s)
                }
            }
        }
          , B = function() {
            return n.nc
        }
          , Y = function(e) {
            var t = document.head
              , n = e || t
              , r = document.createElement("style")
              , i = function(e) {
                for (var t = e.childNodes, n = t.length; n >= 0; n--) {
                    var r = t[n];
                    if (r && 1 === r.nodeType && r.hasAttribute(T))
                        return r
                }
            }(n)
              , o = void 0 !== i ? i.nextSibling : null;
            r.setAttribute(T, "active"),
            r.setAttribute("data-styled-version", "5.3.6");
            var s = B();
            return s && r.setAttribute("nonce", s),
            n.insertBefore(r, o),
            r
        }
          , M = function() {
            function e(e) {
                var t = this.element = Y(e);
                t.appendChild(document.createTextNode("")),
                this.sheet = function(e) {
                    if (e.sheet)
                        return e.sheet;
                    for (var t = document.styleSheets, n = 0, r = t.length; n < r; n++) {
                        var i = t[n];
                        if (i.ownerNode === e)
                            return i
                    }
                    D(17)
                }(t),
                this.length = 0
            }
            var t = e.prototype;
            return t.insertRule = function(e, t) {
                try {
                    return this.sheet.insertRule(t, e),
                    this.length++,
                    !0
                } catch (n) {
                    return !1
                }
            }
            ,
            t.deleteRule = function(e) {
                this.sheet.deleteRule(e),
                this.length--
            }
            ,
            t.getRule = function(e) {
                var t = this.sheet.cssRules[e];
                return void 0 !== t && "string" == typeof t.cssText ? t.cssText : ""
            }
            ,
            e
        }()
          , G = function() {
            function e(e) {
                var t = this.element = Y(e);
                this.nodes = t.childNodes,
                this.length = 0
            }
            var t = e.prototype;
            return t.insertRule = function(e, t) {
                if (e <= this.length && e >= 0) {
                    var n = document.createTextNode(t)
                      , r = this.nodes[e];
                    return this.element.insertBefore(n, r || null),
                    this.length++,
                    !0
                }
                return !1
            }
            ,
            t.deleteRule = function(e) {
                this.element.removeChild(this.nodes[e]),
                this.length--
            }
            ,
            t.getRule = function(e) {
                return e < this.length ? this.nodes[e].textContent : ""
            }
            ,
            e
        }()
          , V = function() {
            function e(e) {
                this.rules = [],
                this.length = 0
            }
            var t = e.prototype;
            return t.insertRule = function(e, t) {
                return e <= this.length && (this.rules.splice(e, 0, t),
                this.length++,
                !0)
            }
            ,
            t.deleteRule = function(e) {
                this.rules.splice(e, 1),
                this.length--
            }
            ,
            t.getRule = function(e) {
                return e < this.length ? this.rules[e] : ""
            }
            ,
            e
        }()
          , H = k
          , F = {
            isServer: !k,
            useCSSOMInjection: !R
        }
          , z = function() {
            function e(e, t, n) {
                void 0 === e && (e = S),
                void 0 === t && (t = {}),
                this.options = _({}, F, {}, e),
                this.gs = t,
                this.names = new Map(n),
                this.server = !!e.isServer,
                !this.server && k && H && (H = !1,
                function(e) {
                    for (var t = document.querySelectorAll(A), n = 0, r = t.length; n < r; n++) {
                        var i = t[n];
                        i && "active" !== i.getAttribute(T) && (j(e, i),
                        i.parentNode && i.parentNode.removeChild(i))
                    }
                }(this))
            }
            e.registerId = function(e) {
                return I(e)
            }
            ;
            var t = e.prototype;
            return t.reconstructWithOptions = function(t, n) {
                return void 0 === n && (n = !0),
                new e(_({}, this.options, {}, t),this.gs,n && this.names || void 0)
            }
            ,
            t.allocateGSInstance = function(e) {
                return this.gs[e] = (this.gs[e] || 0) + 1
            }
            ,
            t.getTag = function() {
                var e, t, n, r, i;
                return this.tag || (this.tag = (n = (t = this.options).isServer,
                r = t.useCSSOMInjection,
                i = t.target,
                e = n ? new V(i) : r ? new M(i) : new G(i),
                new O(e)))
            }
            ,
            t.hasNameForId = function(e, t) {
                return this.names.has(e) && this.names.get(e).has(t)
            }
            ,
            t.registerName = function(e, t) {
                if (I(e),
                this.names.has(e))
                    this.names.get(e).add(t);
                else {
                    var n = new Set;
                    n.add(t),
                    this.names.set(e, n)
                }
            }
            ,
            t.insertRules = function(e, t, n) {
                this.registerName(e, t),
                this.getTag().insertRules(I(e), n)
            }
            ,
            t.clearNames = function(e) {
                this.names.has(e) && this.names.get(e).clear()
            }
            ,
            t.clearRules = function(e) {
                this.getTag().clearGroup(I(e)),
                this.clearNames(e)
            }
            ,
            t.clearTag = function() {
                this.tag = void 0
            }
            ,
            t.toString = function() {
                return function(e) {
                    for (var t = e.getTag(), n = t.length, r = "", i = 0; i < n; i++) {
                        var o, s = (o = i,
                        C.get(o));
                        if (void 0 !== s) {
                            var a = e.names.get(s)
                              , l = t.getGroup(i);
                            if (a && l && a.size) {
                                var u = T + ".g" + i + '[id="' + s + '"]'
                                  , c = "";
                                void 0 !== a && a.forEach(function(e) {
                                    e.length > 0 && (c += e + ",")
                                }),
                                r += "" + l + u + '{content:"' + c + '"}/*!sc*/\n'
                            }
                        }
                    }
                    return r
                }(this)
            }
            ,
            e
        }()
          , q = /(a)(d)/gi
          , W = function(e) {
            return String.fromCharCode(e + (e > 25 ? 39 : 97))
        };
        function J(e) {
            var t, n = "";
            for (t = Math.abs(e); t > 52; t = t / 52 | 0)
                n = W(t % 52) + n;
            return (W(t % 52) + n).replace(q, "$1-$2")
        }
        var K = function(e, t) {
            for (var n = t.length; n; )
                e = 33 * e ^ t.charCodeAt(--n);
            return e
        }
          , X = function(e) {
            return K(5381, e)
        };
        function Z(e) {
            for (var t = 0; t < e.length; t += 1) {
                var n = e[t];
                if (E(n) && !x(n))
                    return !1
            }
            return !0
        }
        var Q = X("5.3.6")
          , ee = function() {
            function e(e, t, n) {
                this.rules = e,
                this.staticRulesId = "",
                this.isStatic = (void 0 === n || n.isStatic) && Z(e),
                this.componentId = t,
                this.baseHash = K(Q, t),
                this.baseStyle = n,
                z.registerId(t)
            }
            return e.prototype.generateAndInjectStyles = function(e, t, n) {
                var r = this.componentId
                  , i = [];
                if (this.baseStyle && i.push(this.baseStyle.generateAndInjectStyles(e, t, n)),
                this.isStatic && !n.hash) {
                    if (this.staticRulesId && t.hasNameForId(r, this.staticRulesId))
                        i.push(this.staticRulesId);
                    else {
                        var o = e_(this.rules, e, t, n).join("")
                          , s = J(K(this.baseHash, o) >>> 0);
                        if (!t.hasNameForId(r, s)) {
                            var a = n(o, "." + s, void 0, r);
                            t.insertRules(r, s, a)
                        }
                        i.push(s),
                        this.staticRulesId = s
                    }
                } else {
                    for (var l = this.rules.length, u = K(this.baseHash, n.hash), c = "", d = 0; d < l; d++) {
                        var p = this.rules[d];
                        if ("string" == typeof p)
                            c += p;
                        else if (p) {
                            var h = e_(p, e, t, n)
                              , f = Array.isArray(h) ? h.join("") : h;
                            u = K(u, f + d),
                            c += f
                        }
                    }
                    if (c) {
                        var g = J(u >>> 0);
                        if (!t.hasNameForId(r, g)) {
                            var m = n(c, "." + g, void 0, r);
                            t.insertRules(r, g, m)
                        }
                        i.push(g)
                    }
                }
                return i.join(" ")
            }
            ,
            e
        }()
          , et = /^\s*\/\/.*$/gm
          , en = [":", "[", ".", "#"];
        function er(e) {
            var t, n, r, i, o = void 0 === e ? S : e, s = o.options, a = o.plugins, l = void 0 === a ? b : a, u = new c(void 0 === s ? S : s), d = [], p = function(e) {
                function t(t) {
                    if (t)
                        try {
                            e(t + "}")
                        } catch (n) {}
                }
                return function(n, r, i, o, s, a, l, u, c, d) {
                    switch (n) {
                    case 1:
                        if (0 === c && 64 === r.charCodeAt(0))
                            return e(r + ";"),
                            "";
                        break;
                    case 2:
                        if (0 === u)
                            return r + "/*|*/";
                        break;
                    case 3:
                        switch (u) {
                        case 102:
                        case 112:
                            return e(i[0] + r),
                            "";
                        default:
                            return r + (0 === d ? "/*|*/" : "")
                        }
                    case -2:
                        r.split("/*|*/}").forEach(t)
                    }
                }
            }(function(e) {
                d.push(e)
            }), h = function(e, r, o) {
                return 0 === r && -1 !== en.indexOf(o[n.length]) || o.match(i) ? e : "." + t
            };
            function f(e, o, s, a) {
                void 0 === a && (a = "&");
                var l = e.replace(et, "");
                return t = a,
                r = RegExp("\\" + (n = o) + "\\b", "g"),
                i = RegExp("(\\" + n + "\\b){2,}"),
                u(s || !o ? "" : o, o && s ? s + " " + o + " { " + l + " }" : l)
            }
            return u.use([].concat(l, [function(e, t, i) {
                2 === e && i.length && i[0].lastIndexOf(n) > 0 && (i[0] = i[0].replace(r, h))
            }
            , p, function(e) {
                if (-2 === e) {
                    var t = d;
                    return d = [],
                    t
                }
            }
            ])),
            f.hash = l.length ? l.reduce(function(e, t) {
                return t.name || D(15),
                K(e, t.name)
            }, 5381).toString() : "",
            f
        }
        var ei = a.createContext()
          , eo = (ei.Consumer,
        a.createContext())
          , es = (eo.Consumer,
        new z)
          , ea = er();
        function el() {
            return (0,
            a.useContext)(ei) || es
        }
        function eu(e) {
            var t = (0,
            a.useState)(e.stylisPlugins)
              , n = t[0]
              , r = t[1]
              , i = el()
              , o = (0,
            a.useMemo)(function() {
                var t = i;
                return e.sheet ? t = e.sheet : e.target && (t = t.reconstructWithOptions({
                    target: e.target
                }, !1)),
                e.disableCSSOMInjection && (t = t.reconstructWithOptions({
                    useCSSOMInjection: !1
                })),
                t
            }, [e.disableCSSOMInjection, e.sheet, e.target])
              , s = (0,
            a.useMemo)(function() {
                return er({
                    options: {
                        prefix: !e.disableVendorPrefixes
                    },
                    plugins: n
                })
            }, [e.disableVendorPrefixes, n]);
            return (0,
            a.useEffect)(function() {
                u()(n, e.stylisPlugins) || r(e.stylisPlugins)
            }, [e.stylisPlugins]),
            a.createElement(ei.Provider, {
                value: o
            }, a.createElement(eo.Provider, {
                value: s
            }, e.children))
        }
        var ec = function() {
            function e(e, t) {
                var n = this;
                this.inject = function(e, t) {
                    void 0 === t && (t = ea);
                    var r = n.name + t.hash;
                    e.hasNameForId(n.id, r) || e.insertRules(n.id, r, t(n.rules, r, "@keyframes"))
                }
                ,
                this.toString = function() {
                    return D(12, String(n.name))
                }
                ,
                this.name = e,
                this.id = "sc-keyframes-" + e,
                this.rules = t
            }
            return e.prototype.getName = function(e) {
                return void 0 === e && (e = ea),
                this.name + e.hash
            }
            ,
            e
        }()
          , ed = /([A-Z])/
          , ep = /([A-Z])/g
          , eh = /^ms-/
          , ef = function(e) {
            return "-" + e.toLowerCase()
        };
        function eg(e) {
            return ed.test(e) ? e.replace(ep, ef).replace(eh, "-ms-") : e
        }
        var em = function(e) {
            return null == e || !1 === e || "" === e
        };
        function e_(e, t, n, r) {
            if (Array.isArray(e)) {
                for (var i, o = [], s = 0, a = e.length; s < a; s += 1)
                    "" !== (i = e_(e[s], t, n, r)) && (Array.isArray(i) ? o.push.apply(o, i) : o.push(i));
                return o
            }
            return em(e) ? "" : x(e) ? "." + e.styledComponentId : E(e) ? "function" != typeof e || e.prototype && e.prototype.isReactComponent || !t ? e : e_(e(t), t, n, r) : e instanceof ec ? n ? (e.inject(n, r),
            e.getName(r)) : e : v(e) ? function e(t, n) {
                var r, i, o = [];
                for (var s in t)
                    t.hasOwnProperty(s) && !em(t[s]) && (Array.isArray(t[s]) && t[s].isCss || E(t[s]) ? o.push(eg(s) + ":", t[s], ";") : v(t[s]) ? o.push.apply(o, e(t[s], s)) : o.push(eg(s) + ": " + (r = s,
                    null == (i = t[s]) || "boolean" == typeof i || "" === i ? "" : "number" != typeof i || 0 === i || r in d ? String(i).trim() : i + "px") + ";"));
                return n ? [n + " {"].concat(o, ["}"]) : o
            }(e) : e.toString()
        }
        var ey = function(e) {
            return Array.isArray(e) && (e.isCss = !0),
            e
        };
        function ev(e) {
            for (var t = arguments.length, n = Array(t > 1 ? t - 1 : 0), r = 1; r < t; r++)
                n[r - 1] = arguments[r];
            return E(e) || v(e) ? ey(e_(y(b, [e].concat(n)))) : 0 === n.length && 1 === e.length && "string" == typeof e[0] ? e : ey(e_(y(e, n)))
        }
        var eb = /[!"#$%&'()*+,./:;<=>?@[\\\]^`{|}~-]+/g
          , eS = /(^-|-$)/g;
        function eE(e) {
            return e.replace(eb, "-").replace(eS, "")
        }
        var ew = function(e) {
            return J(X(e) >>> 0)
        };
        function ex(e) {
            return "string" == typeof e
        }
        var eT = function(e) {
            return "function" == typeof e || "object" == typeof e && null !== e && !Array.isArray(e)
        }
          , ek = a.createContext();
        function eR(e) {
            var t = (0,
            a.useContext)(ek)
              , n = (0,
            a.useMemo)(function() {
                var n;
                return (n = e.theme) ? E(n) ? n(t) : Array.isArray(n) || "object" != typeof n ? D(8) : t ? _({}, t, {}, n) : n : D(14)
            }, [e.theme, t]);
            return e.children ? a.createElement(ek.Provider, {
                value: n
            }, e.children) : null
        }
        ek.Consumer;
        var eD = {}
          , eO = function(e) {
            return function e(t, n, r) {
                if (void 0 === r && (r = S),
                !(0,
                s.isValidElementType)(n))
                    return D(1, String(n));
                var i = function() {
                    return t(n, r, ev.apply(void 0, arguments))
                };
                return i.withConfig = function(i) {
                    return e(t, n, _({}, r, {}, i))
                }
                ,
                i.attrs = function(i) {
                    return e(t, n, _({}, r, {
                        attrs: Array.prototype.concat(r.attrs, i).filter(Boolean)
                    }))
                }
                ,
                i
            }(function e(t, n, r) {
                var i = x(t)
                  , o = !ex(t)
                  , s = n.attrs
                  , l = void 0 === s ? b : s
                  , u = n.componentId
                  , c = void 0 === u ? (v = n.displayName,
                T = n.parentComponentId,
                eD[k = "string" != typeof v ? "sc" : eE(v)] = (eD[k] || 0) + 1,
                R = k + "-" + ew("5.3.6" + k + eD[k]),
                T ? T + "-" + R : R) : u
                  , d = n.displayName
                  , p = void 0 === d ? ex(t) ? "styled." + t : "Styled(" + w(t) + ")" : d
                  , f = n.displayName && n.componentId ? eE(n.displayName) + "-" + n.componentId : n.componentId || c
                  , m = i && t.attrs ? Array.prototype.concat(t.attrs, l).filter(Boolean) : l
                  , y = n.shouldForwardProp;
                i && t.shouldForwardProp && (y = n.shouldForwardProp ? function(e, r, i) {
                    return t.shouldForwardProp(e, r, i) && n.shouldForwardProp(e, r, i)
                }
                : t.shouldForwardProp);
                var v, T, k, R, D, O = new ee(r,f,i ? t.componentStyle : void 0), N = O.isStatic && 0 === l.length, C = function(e, t) {
                    return function(e, t, n, r) {
                        var i, o, s, l, u, c, d, p = e.attrs, f = e.componentStyle, g = e.defaultProps, m = e.foldedComponentIds, y = e.shouldForwardProp, v = e.styledComponentId, b = e.target, w = (i = (0,
                        a.useContext)(ek),
                        void 0 === (o = g) && (o = S),
                        void 0 === (s = t.theme !== o.theme && t.theme || i || o.theme || S) && (s = S),
                        l = _({}, t, {
                            theme: s
                        }),
                        u = {},
                        p.forEach(function(e) {
                            var t, n, r, i = e;
                            for (t in E(i) && (i = i(l)),
                            i)
                                l[t] = u[t] = "className" === t ? (n = u[t],
                                r = i[t],
                                n && r ? n + " " + r : n || r) : i[t]
                        }),
                        [l, u]), x = w[0], T = w[1], k = (c = el(),
                        d = (0,
                        a.useContext)(eo) || ea,
                        r ? f.generateAndInjectStyles(S, c, d) : f.generateAndInjectStyles(x, c, d)), R = T.$as || t.$as || T.as || t.as || b, D = ex(R), O = T !== t ? _({}, t, {}, T) : t, N = {};
                        for (var C in O)
                            "$" !== C[0] && "as" !== C && ("forwardedAs" === C ? N.as = O[C] : (y ? y(C, h, R) : !D || h(C)) && (N[C] = O[C]));
                        return t.style && T.style !== t.style && (N.style = _({}, t.style, {}, T.style)),
                        N.className = Array.prototype.concat(m, v, k !== v ? k : null, t.className, T.className).filter(Boolean).join(" "),
                        N.ref = n,
                        (0,
                        a.createElement)(R, N)
                    }(D, e, t, N)
                };
                return C.displayName = p,
                (D = a.forwardRef(C)).attrs = m,
                D.componentStyle = O,
                D.displayName = p,
                D.shouldForwardProp = y,
                D.foldedComponentIds = i ? Array.prototype.concat(t.foldedComponentIds, t.styledComponentId) : b,
                D.styledComponentId = f,
                D.target = i ? t.target : t,
                D.withComponent = function(t) {
                    var i = n.componentId
                      , o = function(e, t) {
                        if (null == e)
                            return {};
                        var n, r, i = {}, o = Object.keys(e);
                        for (r = 0; r < o.length; r++)
                            t.indexOf(n = o[r]) >= 0 || (i[n] = e[n]);
                        return i
                    }(n, ["componentId"])
                      , s = i && i + "-" + (ex(t) ? t : eE(w(t)));
                    return e(t, _({}, o, {
                        attrs: m,
                        componentId: s
                    }), r)
                }
                ,
                Object.defineProperty(D, "defaultProps", {
                    get: function() {
                        return this._foldedDefaultProps
                    },
                    set: function(e) {
                        this._foldedDefaultProps = i ? function e(t) {
                            for (var n = arguments.length, r = Array(n > 1 ? n - 1 : 0), i = 1; i < n; i++)
                                r[i - 1] = arguments[i];
                            for (var o = 0; o < r.length; o++) {
                                var s, a = r[o];
                                if (eT(a))
                                    for (var l in a)
                                        "__proto__" !== (s = l) && "constructor" !== s && "prototype" !== s && function(t, n, r) {
                                            var i = t[r];
                                            eT(n) && eT(i) ? e(i, n) : t[r] = n
                                        }(t, a[l], l)
                            }
                            return t
                        }({}, t.defaultProps, e) : e
                    }
                }),
                D.toString = function() {
                    return "." + D.styledComponentId
                }
                ,
                o && g()(D, t, {
                    attrs: !0,
                    componentStyle: !0,
                    displayName: !0,
                    foldedComponentIds: !0,
                    shouldForwardProp: !0,
                    styledComponentId: !0,
                    target: !0,
                    withComponent: !0
                }),
                D
            }, e)
        };
        function eN(e) {
            for (var t = arguments.length, n = Array(t > 1 ? t - 1 : 0), r = 1; r < t; r++)
                n[r - 1] = arguments[r];
            var i = ev.apply(void 0, [e].concat(n)).join("")
              , o = ew(i);
            return new ec(o,i)
        }
        ["a", "abbr", "address", "area", "article", "aside", "audio", "b", "base", "bdi", "bdo", "big", "blockquote", "body", "br", "button", "canvas", "caption", "cite", "code", "col", "colgroup", "data", "datalist", "dd", "del", "details", "dfn", "dialog", "div", "dl", "dt", "em", "embed", "fieldset", "figcaption", "figure", "footer", "form", "h1", "h2", "h3", "h4", "h5", "h6", "head", "header", "hgroup", "hr", "html", "i", "iframe", "img", "input", "ins", "kbd", "keygen", "label", "legend", "li", "link", "main", "map", "mark", "marquee", "menu", "menuitem", "meta", "meter", "nav", "noscript", "object", "ol", "optgroup", "option", "output", "p", "param", "picture", "pre", "progress", "q", "rp", "rt", "ruby", "s", "samp", "script", "section", "select", "small", "source", "span", "strong", "style", "sub", "summary", "sup", "table", "tbody", "td", "textarea", "tfoot", "th", "thead", "time", "title", "tr", "track", "u", "ul", "var", "video", "wbr", "circle", "clipPath", "defs", "ellipse", "foreignObject", "g", "image", "line", "linearGradient", "marker", "mask", "path", "pattern", "polygon", "polyline", "radialGradient", "rect", "stop", "svg", "text", "textPath", "tspan"].forEach(function(e) {
            eO[e] = eO(e)
        }),
        (i = (function(e, t) {
            this.rules = e,
            this.componentId = t,
            this.isStatic = Z(e),
            z.registerId(this.componentId + 1)
        }
        ).prototype).createStyles = function(e, t, n, r) {
            var i = r(e_(this.rules, t, n, r).join(""), "")
              , o = this.componentId + e;
            n.insertRules(o, o, i)
        }
        ,
        i.removeStyles = function(e, t) {
            t.clearRules(this.componentId + e)
        }
        ,
        i.renderStyles = function(e, t, n, r) {
            e > 2 && z.registerId(this.componentId + e),
            this.removeStyles(e, n),
            this.createStyles(e, t, n, r)
        }
        ,
        (o = (function() {
            var e = this;
            this._emitSheetCSS = function() {
                var t = e.instance.toString();
                if (!t)
                    return "";
                var n = B();
                return "<style " + [n && 'nonce="' + n + '"', T + '="true"', 'data-styled-version="5.3.6"'].filter(Boolean).join(" ") + ">" + t + "</style>"
            }
            ,
            this.getStyleTags = function() {
                return e.sealed ? D(2) : e._emitSheetCSS()
            }
            ,
            this.getStyleElement = function() {
                if (e.sealed)
                    return D(2);
                var t, n = ((t = {})[T] = "",
                t["data-styled-version"] = "5.3.6",
                t.dangerouslySetInnerHTML = {
                    __html: e.instance.toString()
                },
                t), r = B();
                return r && (n.nonce = r),
                [a.createElement("style", _({}, n, {
                    key: "sc-0-0"
                }))]
            }
            ,
            this.seal = function() {
                e.sealed = !0
            }
            ,
            this.instance = new z({
                isServer: !0
            }),
            this.sealed = !1
        }
        ).prototype).collectStyles = function(e) {
            return this.sealed ? D(2) : a.createElement(eu, {
                sheet: this.instance
            }, e)
        }
        ,
        o.interleaveWithNodeStream = function(e) {
            return D(3)
        }
        ;
        var eC = eO
    },
    71739: function(e) {
        e.exports = {
            area: !0,
            base: !0,
            br: !0,
            col: !0,
            embed: !0,
            hr: !0,
            img: !0,
            input: !0,
            link: !0,
            meta: !0,
            param: !0,
            source: !0,
            track: !0,
            wbr: !0
        }
    },
    47156: function(e, t) {
        "use strict";
        t.Z = {
            common: {
                actionSeeMore: "See more"
            },
            privacyPolicyUpdate: {
                description: "pixiv Inc. has updated the <0>Privacy Policy</0> as of June 13, 2023. <1>Revision History</1>",
                agree: "OK"
            },
            ogp: {
                vroid: {
                    description: 'The VRoid project is a 3D business by Pixiv Inc. with the philosophy of "Make Creativities More Enjoyable"\nThe world of "one person, one avatar" where everyone has their own unique 3D character model and can utilize that character for creative activities and communication. Our mission is to realize that future with the power of technology and creativity.'
                },
                vroidStudio: {
                    description: "3D Modeling, for Everyone! VRoid Studio is an application to create 3D models of humanoid avatars (characters).Create original characters on this intuitive and highly Adaptable Software. Easy to use for everyone!"
                }
            },
            footer: {
                home: "Home",
                vroidMobile: "VRoid Mobile",
                vroidStudio: "VRoid Studio",
                vroidHub: "VRoid Hub",
                vroidSDK: "VRoid SDK",
                vroidWear: "VRoid WEAR",
                aboutVRoid: "About VRoid",
                news: "News",
                vroidHelp: "VRoid Help",
                reportBug: "Report a bug",
                japanese: "日本語",
                english: "English"
            },
            topPage: {
                title: "3D Modeling,for Everyone!",
                description: 'The VRoid project is a 3D business by Pixiv Inc. with the philosophy of "Make Creativities More Enjoyable"\nThe world of "one person, one avatar" where everyone has their own unique 3D character model and can utilize that character for creative activities and communication. Our mission is to realize that future with the power of technology and creativity.\n\nVRoid was born from the 3D modeling software "VRoid Studio" that allows you to create characters as if you were drawing a picture. Currently, we are developing in various fields such as this software, smartphone apps that allow you to easily create avatars, platforms that allow you to post 3D models, developer kits for linking with them, and brand businesses that propose avatar fashion to the world. going.',
                links: {
                    vroidStudio: "The Stable Version of VRoid Studio",
                    promotionMovie: "Promotion movie"
                },
                vroidStudio: {
                    category: "3D Character Creation Software",
                    description: "3D Modeling, for Everyone!"
                },
                vroidHub: "A platform for your 3D characters",
                vroidSdk: "Unity package for developers",
                vroidMobile: "Have fun with your\noriginal 3D characters!"
            },
            studioPage: {
                downloadPlatforms: {
                    title: "Download for free",
                    description: "You can use any version of VRoid Studio for free.\nRead the <0>Terms of Use</0> and <1>Privacy policy</1> before downloading.",
                    steam: {
                        description: "If you would like to use VRoid Studio from your computer, we recommend you download it through Steam.",
                        download: "Download from the Steam store"
                    },
                    ipad: {
                        description: "If you'd like to use VRoid Studio on your iPad, please download it from the App Store."
                    }
                },
                downloadButtons: {
                    title: "Download for free"
                },
                mainVisual: {
                    category: "3D Character Creation Software",
                    title: "3D Modeling,\nfor Everyone!"
                },
                step1: {
                    title: "Create Original Characters\non This Intuitive and\nHighly Adaptable Software\nEasy to Use for Everyone!",
                    section1: {
                        title: "Easy for Beginners too",
                        description: "You can start creating right after download; with many ready-to-use preset items, you won’t need to create anything from scratch. You just need to pick items you like and adjust their parameters!"
                    },
                    section2: {
                        title: "Express Yourself",
                        description: "Not only is 3D modeling on VRoid Studio as easy as drawing on paper, but this software also gives you total freedom to express your originality, customizing minor features down to the finest detail."
                    },
                    section3: {
                        title: "Free to Use",
                        description: "VRoid Studio is free to use for anyone. It’s super-easy to set up, as you just need to download it, and then you’re good to go. Models you create on VRoid Studio are yours to use freely on many different platforms and services."
                    }
                },
                step2: {
                    title: "Customize Your Model’s Body However You Like",
                    section1: {
                        title: "Many Customizable Items",
                        description: "Facial features, hairstyles, outfits, and every other preset item is customizable in shape, color, design, and much more via intuitive sliders."
                    },
                    section2: {
                        title: "Edit your Model Directly, in Real-time",
                        description: "Models are customizable in many ways, and you can check each edit in real-time. Little by little, anyone can design their ideal model."
                    }
                },
                step3: {
                    title: "Combine Templates to Design New Outfits",
                    description: "You can start designing your original outfits by selecting one of the many available templates and editing it.\nYou can also overlay and combine more templates for the perfect silhouette.",
                    section1: {
                        description: "Templates vary from the basics to various arrangements."
                    },
                    section2: {
                        description: "You can also overlay more outfits to get the perfect result.\nOnce you get the hang of how to shape the silhouette, start combining more outfits into one, or simply overlay them for a multi-layered look."
                    }
                },
                step4: {
                    title: "Accessorize with Just One Click",
                    section1: {
                        title: "Glasses and Furry Ears",
                        description: "Have your model wear glasses, or even rabbit or cat ears! New accessories will be coming in the later updates."
                    },
                    section2: {
                        title: "Editable Parameters and Textures",
                        description: "With more than 10 dedicated parameters, freely customize shape, size, and even the smaller details! Use original textures and create your best design so far."
                    }
                },
                step5: {
                    title: "Design Textures\nwith the Pen Tool",
                    description: "The texture editing feature supports pressure sensitivity on pen tablets. A layer feature is also included. You can directly draw both 3D models and UV mapping, to create characters while adding textures in real time. The iPad version of VRoid Studio also supports Apple Pencil."
                },
                step6: {
                    title: "Drawing 3D Hair\nis as Easy as\nDrawing on Paper",
                    description: "Create new chunks of hair with a single stroke, and later edit them to your liking through the parameters. Hair is customizable in infinite ways, and you can set hair bounce individually for each hair chunk."
                },
                step7: {
                    title: "Your Models are Yours to Use Freely",
                    description: "You can set your own terms of use for the data of every model, texture, item, etc you create on VRoid Studio, specifying if you give permission for commercial use, credits, etc. Every model is exportable as VRM files and uploadable to apps that support the format.\n\n* When using the data for models created by pixiv or third parties, please be sure to follow the terms of use and <0>licensing conditions</0>."
                },
                step3Dfigure: {
                    title: "あなたのキャラクターが\nカタチになる。",
                    description: "VRoid Studioで制作したモデルはグッズ制作サービス「pixivFACTORY」にアップロードするだけで、簡単に3Dプリントフィギュアにすることができます。",
                    link: "pixivFACTORY 3Dプリントサービス"
                },
                step8: {
                    title: "Create, Connect, Expand",
                    description: "You can upload models you created to VRoid Hub, letting the community view them and send their appreciation. Characters uploaded to VRoid Hub can also be called up in various integrated games and platforms!",
                    actionSeeMore: "Visit VRoid Hub"
                },
                letsVroidStudio: {
                    title: "Let's get started with VRoid Studio!",
                    tutorial: "Tutorial",
                    youtube: "YouTube Channel"
                },
                spec: {
                    windows: {
                        os: {
                            label: "OS",
                            value: "Windows 8.1 / 10 / 11"
                        },
                        cpu: {
                            label: "CPU",
                            value: "Intel Core i5 6th gen or later\nAMD Ryzen 5 3rd gen or later"
                        },
                        memory: {
                            label: "Memory",
                            value: "8 GB RAM"
                        },
                        graphics: {
                            label: "Graphics",
                            value: "Intel Iris Graphics 540 or higher"
                        },
                        storage: {
                            label: "Storage",
                            value: "10 GB available space"
                        }
                    },
                    mac: {
                        os: {
                            label: "OS",
                            value: "macOS 11"
                        },
                        releaseDate: {
                            label: "Year model",
                            value: "2015 models or later"
                        },
                        cpu: {
                            label: "CPU",
                            value: "Intel Core i5 6th gen or later"
                        },
                        memory: {
                            label: "Memory",
                            value: "8 GB RAM"
                        },
                        storage: {
                            label: "Storage",
                            value: "10 GB available space"
                        }
                    },
                    ipad: {
                        os: {
                            label: "OS",
                            value: "iPad OS 15 or later"
                        },
                        releaseDate: {
                            label: "Year model",
                            value: "2018 models or later"
                        },
                        description: "Please refer to <0>Operating environment requirements (required specifications)</0> to learn more about supported devices."
                    }
                },
                creators: {
                    title: "Creators cooperating with the development of VRoid Studio"
                },
                screenshotAlt: "A screenshot of VRoid Studio"
            },
            studio: {
                links: {
                    releaseNotes: "https://vroid.pixiv.help/hc/en-us/sections/360002273834",
                    policiesVroidStudio: "https://policies.pixiv.net/en.html#vroidstudio",
                    policiesPrivacy: "https://policies.pixiv.net/en.html#privacy",
                    privacyPolicy: "https://vroid.pixiv.help/hc/en-us/articles/900007188203",
                    windowsMigrateLink: "https://vroid.pixiv.help/hc/en-us/articles/900001076943",
                    basicUsageLink: "https://vroid.pixiv.help/hc/en-us/categories/360000053442-VRoid-Studio",
                    techniqueLink: "https://vroid.pixiv.help/hc/en-us/sections/360000076662",
                    requirements: "https://vroid.pixiv.help/hc/en-us/articles/900006049066",
                    iPadTextureNotice: "https://vroid.pixiv.help/hc/en-us/articles/22212988393881",
                    aboutiPadEdition: "https://vroid.pixiv.help/hc/en-us/articles/21828351684889"
                },
                ogp: {
                    description: "VRoid Studio is an application to create 3D models of humanoid avatars (characters). The app runs on Windows, macOS, and iPad and can be used for free by anyone. 3D models created with VRoid Studio can be used as avatars on various VR/AR contents for commercial and non-commercial use."
                },
                container: {
                    archiveHeader: "Past versions",
                    installer: "Windows, macOS installers",
                    windows: "Windows",
                    win64bitins: "Windows (64-bit) <0></0> <1>installer</1>",
                    win64bit: "Windows (64-bit) <0></0> <1>zip archive</1>",
                    macos: "macOS"
                },
                title: "VRoid Studio Beta",
                versionInfo: "About this version/Release history",
                privacyPolicyAgreement: "Read the <0>Terms of Use</0> and <1>Privacy policy</1> before downloading.",
                windowsMigrateAttention: "<0>Notes on upgrading from VRoid Studio v0.8.3 or earlier on Windows.</0>",
                forBeginnersTitle: "New to VRoid Studio?",
                basicUsage: "Basics",
                technique: "Handy techniques",
                newsLetter: null,
                newsLetterDescription: "VRoid Studioのアップデートのお知らせや、VRoidプロジェクトの最新情報をお届けします。",
                iPadTextureNotice: "<0>[Important]</0> About Texture Display Resolution on VRoid Studio for iPad",
                downloadBeta: "Download  VRoid Studio beta"
            }
        }
    },
    54399: function(e, t) {
        "use strict";
        t.Z = {
            common: {
                actionSeeMore: "もっと見る"
            },
            privacyPolicyUpdate: {
                description: "ピクシブ株式会社は2023年6月13日付で<0>プライバシーポリシー</0>を改定しました。 <1>改訂履歴</1>",
                agree: "同意"
            },
            ogp: {
                vroid: {
                    description: "VRoidプロジェクトは、「創作活動がもっと楽しくなる場所を創る」を理念とするピクシブ株式会社による3D事業です。誰もが個性豊かな自分の3Dキャラクターモデルを持ち、そのキャラクターを創作活動やコミュニケーションに活用することができる「1人1アバター」の世界。私たちのミッションは、その未来をテクノロジーとクリエイティブの力で実現することです。"
                },
                vroidStudio: {
                    description: "3D創作を誰でも楽しめる世界へ。VRoid Studioは3Dキャラクター制作ソフトウェアです。はじめての人にはかんたんに、慣れた人はよりこだわって、3Dキャラクターを作ることができることができます。"
                }
            },
            footer: {
                home: "ホーム",
                vroidMobile: "VRoid Mobile",
                vroidStudio: "VRoid Studio",
                vroidHub: "VRoid Hub",
                vroidSDK: "VRoid SDK",
                vroidWear: "VRoid WEAR",
                aboutVRoid: "VRoidとは",
                news: "ニュース",
                vroidHelp: "VRoidヘルプ",
                reportBug: "バグを報告",
                japanese: "日本語",
                english: "English"
            },
            topPage: {
                title: "3D創作を誰でも楽しめる世界へ",
                description: "VRoidプロジェクトは、「創作活動がもっと楽しくなる場所を創る」を理念とするピクシブ株式会社による3D事業です。\n誰もが個性豊かな自分の3Dキャラクターモデルを持ち、そのキャラクターを創作活動やコミュニケーションに活用することができる「1人1アバター」の世界。私たちのミッションは、その未来をテクノロジーとクリエイティブの力で実現することです。\n\nVRoidは、絵を描くようにキャラクターを作ることができる3Dモデリングソフトウェア「VRoid Studio」から生まれました。現在はこのソフトウェアをはじめとし、手軽にアバターづくりを楽しめるスマートフォンアプリや、3Dモデルを投稿できるプラットフォーム、それと連携するための開発者キット、アバターファッションを世の中に提案するブランド事業など、多方面で展開を行っています。",
                vroidStudio: {
                    category: "3Dキャラクター制作ソフトウェア",
                    description: "3D創作を誰でも楽しめる世界へ。"
                },
                links: {
                    vroidStudio: "VRoid Studio正式版 配信中",
                    promotionMovie: "プロモーションムービー公開中"
                },
                vroidHub: "3Dキャラクターのためのプラットフォーム",
                vroidSdk: "開発者向けUnity Package",
                vroidMobile: "あなただけの\nオリジナル3Dキャラで遊ぼう！"
            },
            studioPage: {
                downloadPlatforms: {
                    title: "無料でダウンロード",
                    description: "VRoid Studioはどのバージョンも無料でご利用いただけます。\n<0>利用規約</0>・<1>プライバシーポリシー</1>に合意の上、ダウンロードしてください。",
                    steam: {
                        description: "PCでご利用の方はSteamからのダウンロードがおすすめです。",
                        download: "STEAMストアからダウンロード"
                    },
                    ipad: {
                        description: "iPadでご利用の方はApp Storeからダウンロードしてください。"
                    }
                },
                downloadButtons: {
                    title: "無料でダウンロード"
                },
                mainVisual: {
                    category: "3Dキャラクター制作ソフトウェア",
                    title: "3D創作を誰でも\n楽しめる世界へ。"
                },
                step1: {
                    title: "直感的な操作感と高いカスタマイズ性\n初心者から上級者まで\n自分だけの\nオリジナルキャラクターがつくれる",
                    section1: {
                        title: "3D初心者でも簡単",
                        description: "たくさんのプリセットアイテムとパラメータを搭載。ゼロからモデリングをしなくても、アイテムを選んで組み合わせ、パラメータを調整するだけでキャラクターメイキングができます。"
                    },
                    section2: {
                        title: "オリジナリティを表現",
                        description: "絵を描くように髪型を直感的にモデリングできるだけでなく、3Dモデルに直接デザインを描いて、こだわりの表情や瞳、服のデザインを制作可能。普段のお絵かき感覚で3D創作に取り組むことができます。"
                    },
                    section3: {
                        title: "無料で利用可能",
                        description: "VRoid Studioの利用は無料。煩雑なセットアップもなく、すぐにインストールして始められます。もちろん制作したモデルもさまざまな用途で無料で使うことができます。"
                    }
                },
                step2: {
                    title: "キャラクター素体を自由にカスタマイズ",
                    section1: {
                        title: "カスタマイズ可能なたくさんのアイテム",
                        description: "顔パーツ・髪型・服などに、形・大きさ・長さなどを個別に設定できるパラメータが多数用意されています。"
                    },
                    section2: {
                        title: "細かく直感的に変更できる顔・身体",
                        description: "キャラクターデザインを特徴づける顔と身体には、アレンジのためのパラメータが充実。あなたが思い描く理想を直感的に実現できます。"
                    }
                },
                step3: {
                    title: "テンプレートを選んで服をデザイン",
                    description: "様々なテンプレートから好みの形を選んで服を作成することができます。\n複数のテンプレートを組み合わせることも可能です。",
                    section1: {
                        description: "基本となるテンプレートの他にも、さまざまなアレンジテンプレートもご用意しています。"
                    },
                    section2: {
                        description: "服を組み合わせて複数枚着る「重ね着」も可能です。\nシルエットをつくり込んだり、コーディネートを工夫したり、よりこだわった服を作ることができます。"
                    }
                },
                step4: {
                    title: "アクセサリーをワンクリックで追加",
                    section1: {
                        title: "メガネ・けもみみ",
                        description: "メガネとねこみみ、うさみみを装着することができます。今後も様々なアクセサリーの追加を予定しています。"
                    },
                    section2: {
                        title: "パラメータ・テクスチャも変更可能",
                        description: "形、長さ、丸みなど10以上のパラメータを用いて、自由に形を変えられます。テクスチャ変更も可能で、理想の質感やデザインを反映できます。"
                    }
                },
                step5: {
                    title: "本格ペンツールで\n思い通りに\nテクスチャを描き込み",
                    description: "テクスチャ編集機能はペンタブレットの筆圧感知に対応。レイヤー分け機能も搭載されています。3DモデルとUV展開どちらへも直接描くことができ、リアルタイムにテクスチャを描き込んでキャラクターを制作することができます。iPad版はApple Pencilにも対応しています。"
                },
                step6: {
                    title: "絵を描くように\n髪型をモデリング",
                    description: "カーソルを動かすだけで毛束を作ることができ、各種パラメータを調整して太さや向き、毛先のカールといった立体的な特徴を簡単に形作ることができます。髪を揺らすための「ボーン」も手軽に設定可能です。"
                },
                step7: {
                    title: "制作したキャラクターモデルは自由に利用可能",
                    description: "制作した3Dモデルデータやテクスチャ・アイテムデータは、商用・非商用を問わずさまざまな用途に利用可能です。制作したモデルデータはVRM形式でエクスポートすることができ、VRMに対応した各種3Dアプリケーションですぐにご利用いただけます。\n※ピクシブや第三者のデータを用いて制作した場合はライセンス条件に則ってご利用ください。詳しくは、こちらの<0>ガイドライン</0>をご覧ください。"
                },
                step3Dfigure: {
                    title: "あなたのキャラクターが\nカタチになる。",
                    description: "VRoid Studioで制作したモデルはグッズ制作サービス「pixivFACTORY」にアップロードするだけで、簡単に3Dプリントフィギュアにすることができます。",
                    link: "pixivFACTORY 3Dプリントサービス"
                },
                step8: {
                    title: "モデルがつなぐ“輪”\n広がる“遊び”",
                    description: "制作したモデルを3Dキャラクターの投稿・共有プラットフォームVRoid Hubへアップロードすることで、たくさんの人にお披露目できます。また、VRoid Hubを通して、連携したゲームやアプリでお気に入りのキャラクターを使って遊ぶことができます。",
                    actionSeeMore: "VRoid Hubを見る"
                },
                letsVroidStudio: {
                    title: "VRoid Studioを始めよう！",
                    tutorial: "チュートリアル",
                    youtube: "YouTubeチャンネル"
                },
                spec: {
                    windows: {
                        os: {
                            label: "対応OS",
                            value: "Windows 8.1 / 10 / 11"
                        },
                        cpu: {
                            label: "CPU",
                            value: "Intel Core i5 第6世代 以降\nAMD Ryzen 5 第3世代 以降"
                        },
                        memory: {
                            label: "メモリ",
                            value: "8 GB RAM"
                        },
                        graphics: {
                            label: "グラフィック",
                            value: "Intel Iris Graphics 540 以上"
                        },
                        storage: {
                            label: "ストレージ",
                            value: "10 GB 利用可能"
                        }
                    },
                    mac: {
                        os: {
                            label: "対応OS",
                            value: "macOS 11"
                        },
                        releaseDate: {
                            label: "発売時期",
                            value: "2015年 以降発売モデル"
                        },
                        cpu: {
                            label: "CPU",
                            value: "Intel Core i5 第6世代 以降"
                        },
                        memory: {
                            label: "メモリ",
                            value: "8GB RAM"
                        },
                        storage: {
                            label: "ストレージ",
                            value: "10GB 利用可能"
                        }
                    },
                    ipad: {
                        os: {
                            label: "対応OS",
                            value: "iPad OS 15 以降"
                        },
                        releaseDate: {
                            label: "発売時期",
                            value: "2018年 以降発売モデル"
                        },
                        description: "詳しい対応端末は<0>VRoid Studioの動作環境</0>を確認してください。"
                    }
                },
                creators: {
                    title: "開発協力クリエイター"
                },
                screenshotAlt: "VRoid Studioのスクリーンショット"
            },
            studio: {
                links: {
                    releaseNotes: "https://vroid.pixiv.help/hc/ja/sections/360002273834",
                    policiesVroidStudio: "https://policies.pixiv.net/#vroidstudio",
                    policiesPrivacy: "https://policies.pixiv.net/#privacy",
                    privacyPolicy: "https://vroid.pixiv.help/hc/ja/articles/900007188203",
                    windowsMigrateLink: "https://vroid.pixiv.help/hc/ja/articles/900001076943",
                    basicUsageLink: "https://vroid.pixiv.help/hc/ja/categories/360000053442-VRoid-Studio",
                    techniqueLink: "https://vroid.pixiv.help/hc/ja/sections/360000076662",
                    requirements: "https://vroid.pixiv.help/hc/ja/articles/900006049066",
                    iPadTextureNotice: "https://vroid.pixiv.help/hc/ja/articles/22212988393881",
                    aboutiPadEdition: "https://vroid.pixiv.help/hc/ja/articles/21828351684889"
                },
                container: {
                    archiveHeader: "過去のバージョン",
                    installer: "Windows・macOSインストーラー",
                    windows: "Windows版",
                    win64bitins: "Windows 64bit版 <0></0> <1>インストーラ</1>",
                    win64bit: "Windows 64bit版 <0></0> <1>zip圧縮</1>",
                    macos: "macOS版"
                },
                ogp: {
                    description: "VRoid Studioは、人型アバター（キャラクター）の3Dモデルを作成できるWindows・macOS・iPad用アプリケーションで、どなたでも無償でご利用いただけます。作成した3Dモデルは、VR/ARコンテンツ内でアバターとして利用するなど、商用・非商用を問わず、さまざまな用途に活用できます。"
                },
                title: "VRoid Studio ベータ版",
                versionInfo: "バージョン情報 / リリースノート",
                privacyPolicyAgreement: "<0>利用規約</0>・<1>プライバシーポリシー</1>に合意の上、<2></2>ダウンロードしてください。",
                windowsMigrateAttention: "<0>Windows環境でVRoid Studio v0.8.3以前から移行する際の注意点</0>",
                forBeginnersTitle: "初めての方へ",
                basicUsage: "基本的な使い方",
                technique: "便利なテクニック集",
                newsLetter: "ニュースレター",
                newsLetterDescription: "VRoid Studioのアップデートのお知らせや、VRoidプロジェクトの最新情報をお届けします。",
                registerNewsLetter: "ニュースレター登録",
                iPadTextureNotice: "<0>【重要】</0>VRoid Studio iPad版の「テクスチャ編集の表示解像度設定」について",
                downloadBeta: "VRoid Studio ベータ版のダウンロード"
            }
        }
    },
    7297: function(e, t, n) {
        "use strict";
        function r(e, t) {
            return t || (t = e.slice(0)),
            Object.freeze(Object.defineProperties(e, {
                raw: {
                    value: Object.freeze(t)
                }
            }))
        }
        n.d(t, {
            Z: function() {
                return r
            }
        })
    },
    17527: function(e, t, n) {
        "use strict";
        let r;
        n.d(t, {
            a3: function() {
                return P
            },
            cC: function() {
                return C
            },
            Db: function() {
                return D
            },
            $G: function() {
                return I
            }
        });
        var i = n(67294);
        function o() {
            return (o = Object.assign ? Object.assign.bind() : function(e) {
                for (var t = 1; t < arguments.length; t++) {
                    var n = arguments[t];
                    for (var r in n)
                        Object.prototype.hasOwnProperty.call(n, r) && (e[r] = n[r])
                }
                return e
            }
            ).apply(this, arguments)
        }
        var s = n(71739)
          , a = n.n(s)
          , l = /\s([^'"/\s><]+?)[\s/>]|([^\s=]+)=\s?(".*?"|'.*?')/g;
        function u(e) {
            var t = {
                type: "tag",
                name: "",
                voidElement: !1,
                attrs: {},
                children: []
            }
              , n = e.match(/<\/?([^\s]+?)[/\s>]/);
            if (n && (t.name = n[1],
            (a()[n[1]] || "/" === e.charAt(e.length - 2)) && (t.voidElement = !0),
            t.name.startsWith("!--"))) {
                var r = e.indexOf("-->");
                return {
                    type: "comment",
                    comment: -1 !== r ? e.slice(4, r) : ""
                }
            }
            for (var i = RegExp(l), o = null; null !== (o = i.exec(e)); )
                if (o[0].trim()) {
                    if (o[1]) {
                        var s = o[1].trim()
                          , u = [s, ""];
                        s.indexOf("=") > -1 && (u = s.split("=")),
                        t.attrs[u[0]] = u[1],
                        i.lastIndex--
                    } else
                        o[2] && (t.attrs[o[2]] = o[3].trim().substring(1, o[3].length - 1))
                }
            return t
        }
        var c = /<[a-zA-Z0-9\-\!\/](?:"[^"]*"|'[^']*'|[^'">])*>/g
          , d = /^\s*$/
          , p = Object.create(null)
          , h = {
            parse: function(e, t) {
                t || (t = {}),
                t.components || (t.components = p);
                var n, r = [], i = [], o = -1, s = !1;
                if (0 !== e.indexOf("<")) {
                    var a = e.indexOf("<");
                    r.push({
                        type: "text",
                        content: -1 === a ? e : e.substring(0, a)
                    })
                }
                return e.replace(c, function(a, l) {
                    if (s) {
                        if (a !== "</" + n.name + ">")
                            return;
                        s = !1
                    }
                    var c, p = "/" !== a.charAt(1), h = a.startsWith("<!--"), f = l + a.length, g = e.charAt(f);
                    if (h) {
                        var m = u(a);
                        return o < 0 ? (r.push(m),
                        r) : ((c = i[o]).children.push(m),
                        r)
                    }
                    if (p && (o++,
                    "tag" === (n = u(a)).type && t.components[n.name] && (n.type = "component",
                    s = !0),
                    n.voidElement || s || !g || "<" === g || n.children.push({
                        type: "text",
                        content: e.slice(f, e.indexOf("<", f))
                    }),
                    0 === o && r.push(n),
                    (c = i[o - 1]) && c.children.push(n),
                    i[o] = n),
                    (!p || n.voidElement) && (o > -1 && (n.voidElement || n.name === a.slice(2, -1)) && (n = -1 == --o ? r : i[o]),
                    !s && "<" !== g && g)) {
                        c = -1 === o ? r : i[o].children;
                        var _ = e.indexOf("<", f)
                          , y = e.slice(f, -1 === _ ? void 0 : _);
                        d.test(y) && (y = " "),
                        (_ > -1 && o + c.length >= 0 || " " !== y) && c.push({
                            type: "text",
                            content: y
                        })
                    }
                }),
                r
            },
            stringify: function(e) {
                return e.reduce(function(e, t) {
                    return e + function e(t, n) {
                        switch (n.type) {
                        case "text":
                            return t + n.content;
                        case "tag":
                            return t += "<" + n.name + (n.attrs ? function(e) {
                                var t = [];
                                for (var n in e)
                                    t.push(n + '="' + e[n] + '"');
                                return t.length ? " " + t.join(" ") : ""
                            }(n.attrs) : "") + (n.voidElement ? "/>" : ">"),
                            n.voidElement ? t : t + n.children.reduce(e, "") + "</" + n.name + ">";
                        case "comment":
                            return t + "<!--" + n.comment + "-->"
                        }
                    }("", t)
                }, "")
            }
        };
        function f() {
            if (console && console.warn) {
                for (var e = arguments.length, t = Array(e), n = 0; n < e; n++)
                    t[n] = arguments[n];
                "string" == typeof t[0] && (t[0] = `react-i18next:: ${t[0]}`),
                console.warn(...t)
            }
        }
        let g = {};
        function m() {
            for (var e = arguments.length, t = Array(e), n = 0; n < e; n++)
                t[n] = arguments[n];
            "string" == typeof t[0] && g[t[0]] || ("string" == typeof t[0] && (g[t[0]] = new Date),
            f(...t))
        }
        let _ = (e,t)=>()=>{
            if (e.isInitialized)
                t();
            else {
                let n = ()=>{
                    setTimeout(()=>{
                        e.off("initialized", n)
                    }
                    , 0),
                    t()
                }
                ;
                e.on("initialized", n)
            }
        }
        ;
        function y(e, t, n) {
            e.loadNamespaces(t, _(e, n))
        }
        function v(e, t, n, r) {
            "string" == typeof n && (n = [n]),
            n.forEach(t=>{
                0 > e.options.ns.indexOf(t) && e.options.ns.push(t)
            }
            ),
            e.loadLanguages(t, _(e, r))
        }
        let b = /&(?:amp|#38|lt|#60|gt|#62|apos|#39|quot|#34|nbsp|#160|copy|#169|reg|#174|hellip|#8230|#x2F|#47);/g
          , S = {
            "&amp;": "&",
            "&#38;": "&",
            "&lt;": "<",
            "&#60;": "<",
            "&gt;": ">",
            "&#62;": ">",
            "&apos;": "'",
            "&#39;": "'",
            "&quot;": '"',
            "&#34;": '"',
            "&nbsp;": " ",
            "&#160;": " ",
            "&copy;": "\xa9",
            "&#169;": "\xa9",
            "&reg;": "\xae",
            "&#174;": "\xae",
            "&hellip;": "…",
            "&#8230;": "…",
            "&#x2F;": "/",
            "&#47;": "/"
        }
          , E = e=>S[e]
          , w = e=>e.replace(b, E)
          , x = {
            bindI18n: "languageChanged",
            bindI18nStore: "",
            transEmptyNodeValue: "",
            transSupportBasicHtmlNodes: !0,
            transWrapTextNodes: "",
            transKeepBasicHtmlNodesFor: ["br", "strong", "i", "p"],
            useSuspense: !0,
            unescape: w
        };
        function T(e, t) {
            if (!e)
                return !1;
            let n = e.props ? e.props.children : e.children;
            return t ? n.length > 0 : !!n
        }
        function k(e) {
            if (!e)
                return [];
            let t = e.props ? e.props.children : e.children;
            return e.props && e.props.i18nIsDynamicList ? R(t) : t
        }
        function R(e) {
            return Array.isArray(e) ? e : [e]
        }
        let D = {
            type: "3rdParty",
            init(e) {
                !function() {
                    let e = arguments.length > 0 && void 0 !== arguments[0] ? arguments[0] : {};
                    x = {
                        ...x,
                        ...e
                    }
                }(e.options.react),
                r = e
            }
        }
          , O = (0,
        i.createContext)();
        class N {
            constructor() {
                this.usedNamespaces = {}
            }
            addUsedNamespaces(e) {
                e.forEach(e=>{
                    this.usedNamespaces[e] || (this.usedNamespaces[e] = !0)
                }
                )
            }
            getUsedNamespaces() {
                return Object.keys(this.usedNamespaces)
            }
        }
        function C(e) {
            let {children: t, count: n, parent: s, i18nKey: a, context: l, tOptions: u={}, values: c, defaults: d, components: p, ns: g, i18n: _, t: y, shouldUnescape: v, ...b} = e
              , {i18n: S, defaultNS: E} = (0,
            i.useContext)(O) || {}
              , w = _ || S || r
              , D = y || w && w.t.bind(w);
            return function(e) {
                let {children: t, count: n, parent: s, i18nKey: a, context: l, tOptions: u={}, values: c, defaults: d, components: p, ns: g, i18n: _, t: y, shouldUnescape: v, ...b} = e
                  , S = _ || r;
                if (!S)
                    return m("You will need to pass in an i18next instance by using i18nextReactModule"),
                    t;
                let E = y || S.t.bind(S) || (e=>e);
                l && (u.context = l);
                let w = {
                    ...x,
                    ...S.options && S.options.react
                }
                  , D = g || E.ns || S.options && S.options.defaultNS;
                D = "string" == typeof D ? [D] : D || ["translation"];
                let O = function e(t, n) {
                    if (!t)
                        return "";
                    let r = ""
                      , o = R(t)
                      , s = n.transSupportBasicHtmlNodes && n.transKeepBasicHtmlNodesFor ? n.transKeepBasicHtmlNodesFor : [];
                    return o.forEach((t,o)=>{
                        if ("string" == typeof t)
                            r += `${t}`;
                        else if ((0,
                        i.isValidElement)(t)) {
                            let a = Object.keys(t.props).length
                              , l = s.indexOf(t.type) > -1
                              , u = t.props.children;
                            if (!u && l && 0 === a)
                                r += `<${t.type}/>`;
                            else if (u || l && 0 === a) {
                                if (t.props.i18nIsDynamicList)
                                    r += `<${o}></${o}>`;
                                else if (l && 1 === a && "string" == typeof u)
                                    r += `<${t.type}>${u}</${t.type}>`;
                                else {
                                    let c = e(u, n);
                                    r += `<${o}>${c}</${o}>`
                                }
                            } else
                                r += `<${o}></${o}>`
                        } else if (null === t)
                            f("Trans: the passed in value is invalid - seems you passed in a null child.");
                        else if ("object" == typeof t) {
                            let {format: d, ...p} = t
                              , h = Object.keys(p);
                            if (1 === h.length) {
                                let g = d ? `${h[0]}, ${d}` : h[0];
                                r += `{{${g}}}`
                            } else
                                f("react-i18next: the passed in object contained more than one variable - the object should look like {{ value, format }} where format is optional.", t)
                        } else
                            f("Trans: the passed in value is invalid - seems you passed in a variable like {number} - please pass in variables for interpolation as full objects like {{number}}.", t)
                    }
                    ),
                    r
                }(t, w)
                  , N = d || O || w.transEmptyNodeValue || a
                  , {hashTransKey: C} = w
                  , $ = a || (C ? C(O || N) : O || N)
                  , I = c ? u.interpolation : {
                    interpolation: {
                        ...u.interpolation,
                        prefix: "#$?",
                        suffix: "?$#"
                    }
                }
                  , P = {
                    ...u,
                    count: n,
                    ...c,
                    ...I,
                    defaultValue: N,
                    ns: D
                }
                  , A = $ ? E($, P) : N
                  , L = function(e, t, n, r, s, a) {
                    if ("" === t)
                        return [];
                    let l = r.transKeepBasicHtmlNodesFor || []
                      , u = t && RegExp(l.map(e=>`<${e}`).join("|")).test(t);
                    if (!e && !u && !a)
                        return [t];
                    let c = {};
                    !function e(t) {
                        let n = R(t);
                        n.forEach(t=>{
                            "string" == typeof t || (T(t) ? e(k(t)) : "object" != typeof t || (0,
                            i.isValidElement)(t) || Object.assign(c, t))
                        }
                        )
                    }(e);
                    let d = h.parse(`<0>${t}</0>`)
                      , p = {
                        ...c,
                        ...s
                    };
                    function f(e, t, n) {
                        let r = k(e)
                          , o = m(r, t.children, n);
                        return "[object Array]" === Object.prototype.toString.call(r) && r.every(e=>(0,
                        i.isValidElement)(e)) && 0 === o.length || e.props && e.props.i18nIsDynamicList ? r : o
                    }
                    function g(e, t, n, r, s) {
                        e.dummy ? (e.children = t,
                        n.push((0,
                        i.cloneElement)(e, {
                            key: r
                        }, s ? void 0 : t))) : n.push(...i.Children.map([e], e=>{
                            let n = {
                                ...e.props
                            };
                            return delete n.i18nIsDynamicList,
                            i.createElement(e.type, o({}, n, {
                                key: r,
                                ref: e.ref
                            }, s ? {} : {
                                children: t
                            }))
                        }
                        ))
                    }
                    function m(t, o, s) {
                        let c = R(t)
                          , d = R(o);
                        return d.reduce((t,o,d)=>{
                            let h = o.children && o.children[0] && o.children[0].content && n.services.interpolator.interpolate(o.children[0].content, p, n.language);
                            if ("tag" === o.type) {
                                let _ = c[parseInt(o.name, 10)];
                                1 !== s.length || _ || (_ = s[0][o.name]),
                                _ || (_ = {});
                                let y = 0 !== Object.keys(o.attrs).length ? function(e, t) {
                                    let n = {
                                        ...t
                                    };
                                    return n.props = Object.assign(e.props, t.props),
                                    n
                                }({
                                    props: o.attrs
                                }, _) : _
                                  , v = (0,
                                i.isValidElement)(y)
                                  , b = v && T(o, !0) && !o.voidElement
                                  , S = u && "object" == typeof y && y.dummy && !v
                                  , E = "object" == typeof e && null !== e && Object.hasOwnProperty.call(e, o.name);
                                if ("string" == typeof y) {
                                    let w = n.services.interpolator.interpolate(y, p, n.language);
                                    t.push(w)
                                } else if (T(y) || b) {
                                    let x = f(y, o, s);
                                    g(y, x, t, d)
                                } else if (S) {
                                    let k = m(c, o.children, s);
                                    g(y, k, t, d)
                                } else if (Number.isNaN(parseFloat(o.name))) {
                                    if (E) {
                                        let R = f(y, o, s);
                                        g(y, R, t, d, o.voidElement)
                                    } else if (r.transSupportBasicHtmlNodes && l.indexOf(o.name) > -1) {
                                        if (o.voidElement)
                                            t.push((0,
                                            i.createElement)(o.name, {
                                                key: `${o.name}-${d}`
                                            }));
                                        else {
                                            let D = m(c, o.children, s);
                                            t.push((0,
                                            i.createElement)(o.name, {
                                                key: `${o.name}-${d}`
                                            }, D))
                                        }
                                    } else if (o.voidElement)
                                        t.push(`<${o.name} />`);
                                    else {
                                        let O = m(c, o.children, s);
                                        t.push(`<${o.name}>${O}</${o.name}>`)
                                    }
                                } else if ("object" != typeof y || v)
                                    g(y, h, t, d, 1 !== o.children.length || !h);
                                else {
                                    let N = o.children[0] ? h : null;
                                    N && t.push(N)
                                }
                            } else if ("text" === o.type) {
                                let C = r.transWrapTextNodes
                                  , $ = a ? r.unescape(n.services.interpolator.interpolate(o.content, p, n.language)) : n.services.interpolator.interpolate(o.content, p, n.language);
                                C ? t.push((0,
                                i.createElement)(C, {
                                    key: `${o.name}-${d}`
                                }, $)) : t.push($)
                            }
                            return t
                        }
                        , [])
                    }
                    let _ = m([{
                        dummy: !0,
                        children: e || []
                    }], d, R(e || []));
                    return k(_[0])
                }(p || t, A, S, w, P, v)
                  , U = void 0 !== s ? s : w.defaultTransParent;
                return U ? (0,
                i.createElement)(U, b, L) : L
            }({
                children: t,
                count: n,
                parent: s,
                i18nKey: a,
                context: l,
                tOptions: u,
                values: c,
                defaults: d,
                components: p,
                ns: g || D && D.ns || E || w && w.options && w.options.defaultNS,
                i18n: w,
                t: y,
                shouldUnescape: v,
                ...b
            })
        }
        let $ = (e,t)=>{
            let n = (0,
            i.useRef)();
            return (0,
            i.useEffect)(()=>{
                n.current = t ? n.current : e
            }
            , [e, t]),
            n.current
        }
        ;
        function I(e) {
            let t = arguments.length > 1 && void 0 !== arguments[1] ? arguments[1] : {}
              , {i18n: n} = t
              , {i18n: o, defaultNS: s} = (0,
            i.useContext)(O) || {}
              , a = n || o || r;
            if (a && !a.reportNamespaces && (a.reportNamespaces = new N),
            !a) {
                m("You will need to pass in an i18next instance by using initReactI18next");
                let l = (e,t)=>"string" == typeof t ? t : t && "object" == typeof t && "string" == typeof t.defaultValue ? t.defaultValue : Array.isArray(e) ? e[e.length - 1] : e
                  , u = [l, {}, !1];
                return u.t = l,
                u.i18n = {},
                u.ready = !1,
                u
            }
            a.options.react && void 0 !== a.options.react.wait && m("It seems you are still using the old wait option, you may migrate to the new useSuspense behaviour.");
            let c = {
                ...x,
                ...a.options.react,
                ...t
            }
              , {useSuspense: d, keyPrefix: p} = c
              , h = e || s || a.options && a.options.defaultNS;
            h = "string" == typeof h ? [h] : h || ["translation"],
            a.reportNamespaces.addUsedNamespaces && a.reportNamespaces.addUsedNamespaces(h);
            let f = (a.isInitialized || a.initializedStoreOnce) && h.every(e=>(function(e, t) {
                let n = arguments.length > 2 && void 0 !== arguments[2] ? arguments[2] : {};
                if (!t.languages || !t.languages.length)
                    return m("i18n.languages were undefined or empty", t.languages),
                    !0;
                let r = void 0 !== t.options.ignoreJSONStructure;
                return r ? t.hasLoadedNamespace(e, {
                    lng: n.lng,
                    precheck: (t,r)=>{
                        if (n.bindI18n && n.bindI18n.indexOf("languageChanging") > -1 && t.services.backendConnector.backend && t.isLanguageChangingTo && !r(t.isLanguageChangingTo, e))
                            return !1
                    }
                }) : function(e, t) {
                    let n = arguments.length > 2 && void 0 !== arguments[2] ? arguments[2] : {}
                      , r = t.languages[0]
                      , i = !!t.options && t.options.fallbackLng
                      , o = t.languages[t.languages.length - 1];
                    if ("cimode" === r.toLowerCase())
                        return !0;
                    let s = (e,n)=>{
                        let r = t.services.backendConnector.state[`${e}|${n}`];
                        return -1 === r || 2 === r
                    }
                    ;
                    return (!(n.bindI18n && n.bindI18n.indexOf("languageChanging") > -1) || !t.services.backendConnector.backend || !t.isLanguageChangingTo || !!s(t.isLanguageChangingTo, e)) && !!(t.hasResourceBundle(r, e) || !t.services.backendConnector.backend || t.options.resources && !t.options.partialBundledLanguages || s(r, e) && (!i || s(o, e)))
                }(e, t, n)
            }
            )(e, a, c));
            function g() {
                return a.getFixedT(t.lng || null, "fallback" === c.nsMode ? h : h[0], p)
            }
            let[_,b] = (0,
            i.useState)(g)
              , S = h.join();
            t.lng && (S = `${t.lng}${S}`);
            let E = $(S)
              , w = (0,
            i.useRef)(!0);
            (0,
            i.useEffect)(()=>{
                let {bindI18n: e, bindI18nStore: n} = c;
                function r() {
                    w.current && b(g)
                }
                return w.current = !0,
                f || d || (t.lng ? v(a, t.lng, h, ()=>{
                    w.current && b(g)
                }
                ) : y(a, h, ()=>{
                    w.current && b(g)
                }
                )),
                f && E && E !== S && w.current && b(g),
                e && a && a.on(e, r),
                n && a && a.store.on(n, r),
                ()=>{
                    w.current = !1,
                    e && a && e.split(" ").forEach(e=>a.off(e, r)),
                    n && a && n.split(" ").forEach(e=>a.store.off(e, r))
                }
            }
            , [a, S]);
            let T = (0,
            i.useRef)(!0);
            (0,
            i.useEffect)(()=>{
                w.current && !T.current && b(g),
                T.current = !1
            }
            , [a, p]);
            let k = [_, a, f];
            if (k.t = _,
            k.i18n = a,
            k.ready = f,
            f || !f && !d)
                return k;
            throw new Promise(e=>{
                t.lng ? v(a, t.lng, h, ()=>e()) : y(a, h, ()=>e())
            }
            )
        }
        function P(e) {
            let {i18n: t, defaultNS: n, children: r} = e
              , o = (0,
            i.useMemo)(()=>({
                i18n: t,
                defaultNS: n
            }), [t, n]);
            return (0,
            i.createElement)(O.Provider, {
                value: o
            }, r)
        }
    }
}, function(e) {
    var t = function(t) {
        return e(e.s = t)
    };
    e.O(0, [774, 179], function() {
        return t(54314),
        t(6840),
        t(80880)
    }),
    _N_E = e.O()
}
]);
