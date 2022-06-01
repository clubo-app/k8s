# USER MINKUBE TUNNEL TO ACCESS LOADBALANCER SERVICE FROM LOCALHOST
# minikube tunnel


# Welcome to Tilt!
#   To get you started as quickly as possible, we have created a
#   starter Tiltfile for you.
#
#   Uncomment, modify, and delete any commands as needed for your
#   project's configuration.

# Build Docker image
#   Tilt will automatically associate image builds with the resource(s)
#   that reference them (e.g. via Kubernetes or Docker Compose YAML).
#
#   More info: https://docs.tilt.dev/api.html#api.docker_build
#
docker_build(
    'jonashiltl/profile-service', 
    '../profile-service', 
    dockerfile='../profile-service/Dockerfile', 
    only=[
        '../profile-service', 
    ],
    live_update=[
        # Sync files from host to container
        sync('../profile-service', '/app'),
    ]
)

docker_build(
    'jonashiltl/auth-service', 
    '../auth-service', 
    dockerfile='../auth-service/Dockerfile', 
    only=[
        '../auth-service', 
    ],
    live_update=[
        # Sync files from host to container
        sync('../auth-service', '/app'),
    ]
)

docker_build(
    'jonashiltl/party-service',
    '../party-service', 
    dockerfile='../party-service/Dockerfile', 
    only=[
        '../party-service', 
    ],
    live_update=[
        sync('../party-service', '/app'),
    ]
)

docker_build(
    'jonashiltl/relation-service', 
    '../relation-service', 
    dockerfile='../relation-service/Dockerfile', 
    only=[
        '../relation-service', 
    ],
    live_update=[
        sync('../relation-service', '/app'),
    ]
)

docker_build(
    'jonashiltl/story-service', 
    '../story-service',
    dockerfile='../story-service/Dockerfile', 
    only=[
        '../story-service', 
    ],
    live_update=[
        sync('../story-service', '/app'),
    ]
)

docker_build(
    'jonashiltl/comment-service',
    '../comment-service', 
    dockerfile='../comment-service/Dockerfile', 
    only=[
        '../comment-service', 
    ],
    live_update=[
        sync('../comment-service', '/app'),
    ]
)

docker_build(
    'jonashiltl/notification-service',
    '../notification-service', 
    dockerfile='../notification-service/Dockerfile', 
    only=[
        '../notification-service', 
    ],
    live_update=[
        sync('../notification-service', '/app'),
    ]
)

docker_build(
    'jonashiltl/aggregator',
    '../aggregator-service', 
    dockerfile='../aggregator-service/Dockerfile', 
    only=[
        '../aggregator-service', 
    ],
    live_update=[
        sync('../aggregator-service', '/app'),
    ]
)

load('ext://helm_remote', 'helm_remote')
helm_remote(
    "nats",
    repo_name='nats',
    repo_url='https://nats-io.github.io/k8s/helm/charts/',
    set=['nats.jetstream.enabled=true'],
)
# Apply Kubernetes manifests
#   Tilt will build & push any necessary images, re-deploying your
#   resources as they change.
#
#   More info: https://docs.tilt.dev/api.html#api.k8s_yaml
#
k8s_yaml([
    'deployments/comment.yaml',
    # 'deployments/notification.yaml',
    'deployments/party.yaml',
    'deployments/profile.yaml',
    'deployments/auth.yaml',
    # 'deployments/story.yaml',
    'deployments/relation.yaml',
    'deployments/aggregator.yaml',
    #'deployments/scylla-sync.yaml',
])
k8s_yaml([
    'services/comment.yaml',
    # 'services/notification.yaml',
    'services/party.yaml',
    # 'services/story.yaml',
    'services/profile.yaml',
    'services/auth.yaml',
    # 'services/vespa.yaml',
    'services/aggregator.yaml',
    'services/relation.yaml',
    #'k8s/services/scylla.yaml',
    #'k8s/services/mongo.yaml',
])
# k8s_yaml([
#    'statefulsets/vespa.yaml', 
#])
#k8s_yaml([
#    'k8s/endpoints/mongo.yaml',
#    'k8s/endpoints/scylla.yaml',
#])

update_settings(suppress_unused_image_warnings=["jonashiltl/story-service", "jonashiltl/notification-service"])


# Customize a Kubernetes resource
#   By default, Kubernetes resource names are automatically assigned
#   based on objects in the YAML manifests, e.g. Deployment name.
#
#   Tilt strives for sane defaults, so calling k8s_resource is
#   optional, and you only need to pass the arguments you want to
#   override.
#
#   More info: https://docs.tilt.dev/api.html#api.k8s_resource
#
# k8s_resource('profile', port_forwards=['8080:8080','8081:8081','8180:8180'])


# Run local commands
#   Local commands can be helpful for one-time tasks like installing
#   project prerequisites. They can also manage long-lived processes
#   for non-containerized services or dependencies.
#
#   More info: https://docs.tilt.dev/local_resource.html
#
# local_resource('install-helm',
#                cmd='which helm > /dev/null || brew install helm',
#                # `cmd_bat`, when present, is used instead of `cmd` on Windows.
#                cmd_bat=[
#                    'powershell.exe',
#                    '-Noninteractive',
#                    '-Command',
#                    '& {if (!(Get-Command helm -ErrorAction SilentlyContinue)) {scoop install helm}}'
#                ]
# )
